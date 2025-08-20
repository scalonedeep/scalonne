
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Galería de Sayago Perros</title>
    <!-- Firebase App (core) -->
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <!-- Firebase Firestore -->
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-firestore-compat.js"></script>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background-color: #0a0a1a;
            color: #f0f0f0;
            line-height: 1.6;
            padding: 20px;
            max-width: 1200px;
            margin: 0 auto;
            background: linear-gradient(135deg, #0a0a1a 0%, #0a122a 100%);
        }
        
        header {
            text-align: center;
            margin-bottom: 30px;
            padding: 20px;
            border-bottom: 1px solid #1a2a6c;
        }
        
        h1 {
            font-size: 2.5rem;
            margin-bottom: 5px;
            color: #00f3ff;
            text-transform: uppercase;
            letter-spacing: 3px;
            text-shadow: 0 0 10px #00f3ff, 0 0 20px #00f3ff;
        }
        
        h2 {
            font-size: 1.5rem;
            margin: 20px 0;
            color: #8be9fd;
        }
        
        .upload-section {
            background-color: #1a1a2e;
            padding: 25px;
            border-radius: 10px;
            margin-bottom: 30px;
            box-shadow: 0 4px 15px rgba(0, 243, 255, 0.2);
            border: 1px solid #1a2a6c;
        }
        
        .file-input-container {
            margin-bottom: 20px;
        }
        
        input[type="file"] {
            display: none;
        }
        
        .file-label {
            display: inline-block;
            padding: 12px 24px;
            background: linear-gradient(to right, #1a2a6c, #00f3ff);
            color: white;
            border-radius: 5px;
            cursor: pointer;
            transition: all 0.3s;
            font-weight: bold;
        }
        
        .file-label:hover {
            background: linear-gradient(to right, #00f3ff, #1a2a6c);
            box-shadow: 0 0 15px rgba(0, 243, 255, 0.5);
        }
        
        .file-name {
            margin-top: 10px;
            color: #8be9fd;
            font-style: italic;
        }
        
        input[type="text"] {
            width: 100%;
            padding: 12px;
            margin: 10px 0 20px;
            background-color: #1a1a2e;
            border: 1px solid #00f3ff;
            border-radius: 5px;
            color: white;
        }
        
        input[type="text"]:focus {
            outline: none;
            box-shadow: 0 0 10px rgba(0, 243, 255, 0.5);
        }
        
        button {
            background: linear-gradient(to right, #1a2a6c, #00f3ff);
            color: #0a0a1a;
            border: none;
            padding: 12px 24px;
            border-radius: 5px;
            cursor: pointer;
            font-weight: bold;
            transition: all 0.3s;
        }
        
        button:hover {
            background: linear-gradient(to right, #00f3ff, #1a2a6c);
            box-shadow: 0 0 15px rgba(0, 243, 255, 0.5);
        }
        
        .gallery {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
            gap: 20px;
            margin-top: 30px;
        }
        
        .gallery-item {
            position: relative;
            overflow: hidden;
            border-radius: 8px;
            box-shadow: 0 4px 15px rgba(0, 243, 255, 0.3);
            transition: all 0.3s;
            border: 1px solid #1a2a6c;
        }
        
        .gallery-item:hover {
            transform: scale(1.03);
            box-shadow: 0 0 20px rgba(0, 243, 255, 0.5);
        }
        
        .gallery-item img {
            width: 100%;
            height: 200px;
            object-fit: cover;
            display: block;
        }
        
        .image-name {
            position: absolute;
            bottom: 0;
            left: 0;
            right: 0;
            background-color: rgba(10, 10, 26, 0.9);
            padding: 8px;
            font-size: 0.9rem;
            text-align: center;
            color: #00f3ff;
        }
        
        .delete-btn {
            position: absolute;
            top: 5px;
            right: 5px;
            background: rgba(255, 0, 0, 0.7);
            color: white;
            border: none;
            border-radius: 50%;
            width: 25px;
            height: 25px;
            cursor: pointer;
            font-size: 14px;
            transition: all 0.3s;
        }
        
        .delete-btn:hover {
            background: rgba(255, 0, 0, 1);
            transform: scale(1.1);
        }
        
        footer {
            text-align: center;
            margin-top: 50px;
            padding: 20px;
            border-top: 1px solid #1a2a6c;
            color: #8be9fd;
            font-size: 0.9rem;
        }
        
        .no-images {
            text-align: center;
            padding: 40px;
            color: #6272a4;
            font-style: italic;
            grid-column: 1 / -1;
        }
        
        .loading {
            display: inline-block;
            width: 20px;
            height: 20px;
            border: 3px solid rgba(0, 243, 255, 0.3);
            border-radius: 50%;
            border-top-color: #00f3ff;
            animation: spin 1s ease-in-out infinite;
        }
        
        @keyframes spin {
            to { transform: rotate(360deg); }
        }
        
        .upload-status {
            margin-left: 15px;
            color: #00f3ff;
        }
        
        .firebase-status {
            margin-top: 15px;
            padding: 10px;
            border-radius: 5px;
            background: rgba(0, 243, 255, 0.1);
            border-left: 4px solid #00f3ff;
        }
        
        /* Responsividad */
        @media (max-width: 768px) {
            .gallery {
                grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
            }
        }
        
        @media (max-width: 480px) {
            h1 {
                font-size: 2rem;
            }
            
            .gallery {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>
    <header>
        <h1>Galería de Sayago Perros</h1>
    </header>
    
    <main>
        <section class="upload-section">
            <h2>Subir archivos</h2>
            <div class="file-input-container">
                <label for="file-upload" class="file-label">Seleccionar archivos</label>
                <input id="file-upload" type="file" multiple accept="image/*">
                <p class="file-name" id="file-name">Sin archivos seleccionados</p>
            </div>
            
            <label for="image-name">Nombre (opcional)</label>
            <input type="text" id="image-name" placeholder="Nombre para la imagen">
            
            <button id="upload-button">Subir fotos</button>
            <span id="upload-status" class="upload-status"></span>
            
            <div id="firebase-status" class="firebase-status">
                🔄 Conectando con la base de datos...
            </div>
        </section>
        
        <h2>Galería</h2>
        <div class="gallery" id="image-gallery">
            <div class="no-images">Cargando imágenes...</div>
        </div>
    </main>
    
    <footer>
        <p>Página hecha por Scalone</p>
        <p>Bono Lomo y Scaloneee 💬</p>
    </footer>

    <script>
        // Clave API de ImgBB (tu clave)
        const IMGBB_API_KEY = '264a8837307c1166637c0f9675b8225c';
        
        // Configuración de Firebase (TUS DATOS - Reemplaza con los tuyos)
        const firebaseConfig = {
            apiKey: "AIzaSyCcM1PfPVbeuruaPOCt-ZzXdw3-cD8NjKc",
            authDomain: "galeriaa-93b29.firebaseapp.com",
            projectId: "galeriaa-93b29",
            storageBucket: "galeriaa-93b29.firebasestorage.app",
            messagingSenderId: "702730781803",
            appId: "1:702730781803:web:5218884538edf056b9dd2e"
        };
        
        // Inicializar Firebase
        let db;
        try {
            firebase.initializeApp(firebaseConfig);
            db = firebase.firestore();
            document.getElementById('firebase-status').innerHTML = '✅ Conectado a la base de datos. Las imágenes serán visibles desde cualquier dispositivo.';
            document.getElementById('firebase-status').style.borderLeftColor = '#00ff00';
        } catch (error) {
            console.error('Error inicializando Firebase:', error);
            document.getElementById('firebase-status').innerHTML = '❌ Error conectando a Firebase. Las imágenes solo serán visibles en este navegador.';
            document.getElementById('firebase-status').style.borderLeftColor = '#ff0000';
        }
        
        document.addEventListener('DOMContentLoaded', function() {
            const fileInput = document.getElementById('file-upload');
            const fileName = document.getElementById('file-name');
            const imageNameInput = document.getElementById('image-name');
            const uploadButton = document.getElementById('upload-button');
            const uploadStatus = document.getElementById('upload-status');
            const gallery = document.getElementById('image-gallery');
            
            // Cargar imágenes al iniciar
            loadImages();
            
            // Mostrar nombre de archivo seleccionado
            fileInput.addEventListener('change', function() {
                if (this.files.length === 0) {
                    fileName.textContent = 'Sin archivos seleccionados';
                } else if (this.files.length === 1) {
                    fileName.textContent = this.files[0].name;
                } else {
                    fileName.textContent = `${this.files.length} archivos seleccionados`;
                }
            });
            
            // Manejar la subida de imágenes
            uploadButton.addEventListener('click', function() {
                if (fileInput.files.length === 0) {
                    alert('Por favor, selecciona al menos una imagen.');
                    return;
                }
                
                // Deshabilitar botón durante la subida
                uploadButton.disabled = true;
                uploadStatus.innerHTML = '<span class="loading"></span> Subiendo...';
                
                // Procesar cada archivo seleccionado
                const uploadPromises = Array.from(fileInput.files).map(file => {
                    return uploadToImgBB(file, imageNameInput.value || file.name);
                });
                
                // Esperar a que todas las subidas terminen
                Promise.all(uploadPromises)
                    .then(results => {
                        // Filtrar solo las subidas exitosas
                        const successfulUploads = results.filter(result => result.success);
                        
                        if (successfulUploads.length > 0) {
                            // Guardar información de las imágenes
                            return saveImageInfo(successfulUploads);
                        } else {
                            throw new Error('Todas las subidas fallaron');
                        }
                    })
                    .then(() => {
                        uploadStatus.textContent = '¡Imágenes subidas correctamente!';
                        // Recargar la galería
                        loadImages();
                    })
                    .catch(error => {
                        console.error('Error al subir imágenes:', error);
                        uploadStatus.textContent = 'Error al subir imágenes. Intenta de nuevo.';
                    })
                    .finally(() => {
                        // Habilitar botón y resetear formulario
                        uploadButton.disabled = false;
                        fileInput.value = '';
                        fileName.textContent = 'Sin archivos seleccionados';
                        imageNameInput.value = '';
                        
                        // Limpiar mensaje de estado después de 3 segundos
                        setTimeout(() => {
                            uploadStatus.textContent = '';
                        }, 3000);
                    });
            });
            
            // Función para subir imagen a ImgBB
            function uploadToImgBB(file, name) {
                return new Promise((resolve, reject) => {
                    const formData = new FormData();
                    formData.append('image', file);
                    if (name) {
                        formData.append('name', name);
                    }
                    
                    fetch(`https://api.imgbb.com/1/upload?key=${IMGBB_API_KEY}`, {
                        method: 'POST',
                        body: formData
                    })
                    .then(response => response.json())
                    .then(data => {
                        if (data.success) {
                            resolve({
                                success: true,
                                name: name || file.name,
                                url: data.data.url,
                                deleteUrl: data.data.delete_url,
                                timestamp: new Date().getTime()
                            });
                        } else {
                            resolve({
                                success: false,
                                error: data.error.message
                            });
                        }
                    })
                    .catch(error => {
                        resolve({
                            success: false,
                            error: error.message
                        });
                    });
                });
            }
            
            // Función para guardar información de la imagen
            function saveImageInfo(images) {
                return new Promise((resolve) => {
                    // Primero intentar guardar en Firebase
                    if (db) {
                        const batch = db.batch();
                        const imagesRef = db.collection('images');
                        
                        images.forEach(image => {
                            const docRef = imagesRef.doc();
                            batch.set(docRef, {
                                name: image.name,
                                url: image.url,
                                timestamp: firebase.firestore.FieldValue.serverTimestamp()
                            });
                        });
                        
                        batch.commit()
                            .then(() => {
                                console.log('Imágenes guardadas en Firebase');
                                // También guardar en localStorage como respaldo
                                saveToLocalStorage(images);
                                resolve();
                            })
                            .catch(error => {
                                console.error('Error guardando en Firebase:', error);
                                // Fallback a localStorage
                                saveToLocalStorage(images);
                                resolve();
                            });
                    } else {
                        // Solo guardar en localStorage si Firebase no está disponible
                        saveToLocalStorage(images);
                        resolve();
                    }
                });
            }
            
            // Función de respaldo para guardar en localStorage
            function saveToLocalStorage(images) {
                let savedImages = JSON.parse(localStorage.getItem('sayagoGalleryImages')) || [];
                savedImages = savedImages.concat(images);
                localStorage.setItem('sayagoGalleryImages', JSON.stringify(savedImages));
            }
            
            // Función para cargar imágenes
            function loadImages() {
                // Primero intentar cargar desde Firebase si está disponible
                if (db) {
                    db.collection('images').orderBy('timestamp', 'desc').get()
                        .then(snapshot => {
                            if (!snapshot.empty) {
                                gallery.innerHTML = '';
                                snapshot.forEach(doc => {
                                    const imageData = doc.data();
                                    addImageToGallery(imageData);
                                });
                            }
                            // También cargar desde localStorage por si hay imágenes más recientes
                            loadFromLocalStorage();
                        })
                        .catch(error => {
                            console.error('Error cargando desde Firebase:', error);
                            // Fallback a localStorage
                            loadFromLocalStorage();
                        });
                } else {
                    // Cargar desde localStorage si Firebase no está disponible
                    loadFromLocalStorage();
                }
            }
            
            // Función para cargar imágenes desde localStorage
            function loadFromLocalStorage() {
                const savedImages = JSON.parse(localStorage.getItem('sayagoGalleryImages')) || [];
                
                if (savedImages.length === 0 && gallery.innerHTML.includes('Cargando')) {
                    gallery.innerHTML = '<div class="no-images">No hay imágenes para mostrar. Sube algunas fotos.</div>';
                    return;
                }
                
                // Solo agregar imágenes si no hay ninguna en la galería
                if (gallery.innerHTML.includes('No hay imágenes')) {
                    gallery.innerHTML = '';
                    savedImages.forEach(imageData => {
                        addImageToGallery(imageData);
                    });
                }
            }
            
            // Función para añadir imagen a la galería
            function addImageToGallery(imageData) {
                const galleryItem = document.createElement('div');
                galleryItem.className = 'gallery-item';
                galleryItem.dataset.id = imageData.timestamp;
                
                const img = document.createElement('img');
                img.src = imageData.url;
                img.alt = imageData.name;
                img.loading = 'lazy';
                
                const nameOverlay = document.createElement('div');
                nameOverlay.className = 'image-name';
                nameOverlay.textContent = imageData.name;
                
                const deleteBtn = document.createElement('button');
                deleteBtn.className = 'delete-btn';
                deleteBtn.innerHTML = 'X';
                deleteBtn.title = 'Eliminar imagen';
                deleteBtn.addEventListener('click', function(e) {
                    e.stopPropagation();
                    deleteImage(imageData);
                });
                
                galleryItem.appendChild(img);
                galleryItem.appendChild(nameOverlay);
                galleryItem.appendChild(deleteBtn);
                gallery.appendChild(galleryItem);
            }
            
            // Función para eliminar imagen
            function deleteImage(imageData) {
                if (confirm('¿Estás seguro de que quieres eliminar esta imagen?')) {
                    // Eliminar de localStorage
                    let savedImages = JSON.parse(localStorage.getItem('sayagoGalleryImages')) || [];
                    savedImages = savedImages.filter(img => img.timestamp !== imageData.timestamp);
                    localStorage.setItem('sayagoGalleryImages', JSON.stringify(savedImages));
                    
                    // Intentar eliminar de Firebase si está disponible
                    if (db) {
                        db.collection('images').where('url', '==', imageData.url).get()
                            .then(snapshot => {
                                snapshot.forEach(doc => {
                                    doc.ref.delete();
                                });
                            })
                            .catch(error => {
                                console.error('Error eliminando de Firebase:', error);
                            });
                    }
                    
                    // Recargar galería
                    loadImages();
                }
            }
        });
    </script>
</body>
</html>
