<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>Aincraft</title>
    <meta name="description" content="Aincraft">
    <script src="https://aframe.io/releases/1.2.0/aframe.min.js"></script>
    <script src="https://cdn.rawgit.com/jeromeetienne/AR.js/2.0.8/aframe/build/aframe-ar.js"></script>
</head>
<body>
    <a-scene embedded arjs="sourceType: webcam;">
        <!-- Objek 3D -->
        <a-box position="0 1.5 -5" color="gray" static-body></a-box>
        <a-box position="0 0 -5" color="blue" static-body></a-box>
        <a-box position="0 -1.5 -5" color="red" static-body></a-box>

        <!-- Kamera -->
        <a-entity camera wasd-controls></a-entity>
        
        <!-- Entity untuk menampilkan gambar dari kamera -->
        <a-entity id="video-container" scale="4 4 -4" position="0 0 -4" material="shader: flat; src: #video"></a-entity>
        <video id="video" autoplay playsinline></video>
    </a-scene>
    
    <script>
        // Mengambil video dari kamera dan menampilkan di elemen video
        navigator.mediaDevices.getUserMedia({ video: true }).then(function(stream) {
            var video = document.getElementById('video');
            video.srcObject = stream;
            video.play();
        });

        // Mendapatkan elemen objek 3D
        var boxes = document.querySelectorAll('a-box');

        // Menambahkan event listener untuk mendeteksi keydown
        document.addEventListener('keydown', function(event) {
            var key = event.key;

            // Menggerakkan setiap objek sesuai dengan tombol yang ditekan
            boxes.forEach(function(box) {
                var currentPosition = box.getAttribute('position');

                switch(key) {
                    case 'w': // Maju
                        currentPosition.z -= 0.1;
                        break;
                    case 's': // Mundur
                        currentPosition.z += 0.1;
                        break;
                    case 'a': // Kiri
                        currentPosition.x -= 0.1;
                        break;
                    case 'd': // Kanan
                        currentPosition.x += 0.1;
                        break;
                    case 'ArrowUp': // Atas
                        currentPosition.y += 0.1;
                        break;
                    case 'ArrowDown': // Bawah
                        currentPosition.y -= 0.1;
                        break;
                }

                // Memperbarui posisi objek
                box.setAttribute('position', currentPosition);
            });
        });
    </script>
</body>
</html> 
