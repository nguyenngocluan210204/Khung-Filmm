# Khung-Filmm<!DOCTYPE html>
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Finndei Frame</title>
    <style>
        body {
            background-color: #121212;
            color: #ffffff;
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
        }

        .container {
            max-width: 800px;
            margin: 20px auto;
            padding: 20px;
            background-color: #1e1e1e;
            border-radius: 10px;
            text-align: center;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Finndei Frame</h1>
        <input type="file" id="upload-image" accept="image/*">
        <input type="file" id="upload-frame" accept="image/*">
        <button id="process-btn">Xử lý ảnh</button>
        <canvas id="canvas" style="margin-top: 20px;"></canvas>
    </div>

    <script>
        document.getElementById('process-btn').addEventListener('click', () => {
            const imageFile = document.getElementById('upload-image').files[0];
            const frameFile = document.getElementById('upload-frame').files[0];
            
            if (!imageFile || !frameFile) {
                alert('Vui lòng tải lên cả ảnh và khung!');
                return;
            }

            const image = new Image();
            const frame = new Image();
            
            image.src = URL.createObjectURL(imageFile);
            frame.src = URL.createObjectURL(frameFile);

            image.onload = () => {
                frame.onload = () => {
                    const canvas = document.getElementById('canvas');
                    const ctx = canvas.getContext('2d');
                    
                    const width = frame.width;
                    const height = frame.height;
                    canvas.width = width;
                    canvas.height = height;
                    
                    // Đổ nền trắng trước khi vẽ ảnh
                    ctx.fillStyle = "#ffffff";
                    ctx.fillRect(0, 0, width, height);
                    
                    // Vẽ ảnh lên nền trắng
                    ctx.drawImage(image, 0, 0, width, height);
                    
                    // Vẽ khung lên trên ảnh
                    ctx.drawImage(frame, 0, 0, width, height);
                };
            };
        });
    </script>
</body>
</html>
