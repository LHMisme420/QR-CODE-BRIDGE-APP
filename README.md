# QR-CODE-BRIDGE-APP
QR CODE BRIDGE
https://lhmisme420.github.io/Bridge-App/qr.html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>QR Code Generator - Bridge App</title>
    <script src="https://cdn.jsdelivr.net/npm/qrcode@1.5.3/build/qrcode.min.js"></script>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }

        .container {
            background: white;
            border-radius: 20px;
            padding: 2rem;
            box-shadow: 0 20px 40px rgba(0,0,0,0.1);
            text-align: center;
            max-width: 500px;
            width: 100%;
        }

        .header {
            margin-bottom: 2rem;
        }

        .header h1 {
            color: #764ba2;
            font-size: 2rem;
            margin-bottom: 0.5rem;
        }

        .header p {
            color: #666;
            font-size: 1.1rem;
        }

        .qr-container {
            margin: 2rem 0;
            padding: 1rem;
            background: #f8f9fa;
            border-radius: 15px;
        }

        #qrcode {
            display: inline-block;
            padding: 20px;
            background: white;
            border-radius: 10px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
        }

        .app-info {
            background: #e8f5e8;
            padding: 1.5rem;
            border-radius: 15px;
            margin: 1.5rem 0;
        }

        .app-info h3 {
            color: #2e7d32;
            margin-bottom: 1rem;
        }

        .features {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 1rem;
            margin: 1.5rem 0;
        }

        .feature {
            display: flex;
            align-items: center;
            gap: 0.5rem;
            font-size: 0.9rem;
        }

        .url-display {
            background: #f1f3f4;
            padding: 1rem;
            border-radius: 10px;
            margin: 1rem 0;
            word-break: break-all;
            font-family: monospace;
        }

        .buttons {
            display: flex;
            gap: 1rem;
            margin-top: 1.5rem;
        }

        .btn {
            flex: 1;
            padding: 1rem;
            border: none;
            border-radius: 10px;
            font-size: 1rem;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .btn-primary {
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white;
        }

        .btn-secondary {
            background: #e9ecef;
            color: #333;
        }

        .btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(0,0,0,0.2);
        }

        .download-btn {
            background: #28a745;
            color: white;
            margin-top: 1rem;
        }

        @media (max-width: 480px) {
            .container {
                padding: 1.5rem;
            }
            
            .features {
                grid-template-columns: 1fr;
            }
            
            .buttons {
                flex-direction: column;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>🌉 Bridge App QR Code</h1>
            <p>Scan to access immediate crisis support</p>
        </div>

        <div class="qr-container">
            <div id="qrcode"></div>
        </div>

        <div class="url-display" id="urlDisplay">
            https://lhmisme420.github.io/Bridge-App/
        </div>

        <div class="app-info">
            <h3>🚨 What's Bridge App?</h3>
            <p>3-click access to crisis support, compassionate listening, and community connection. 100% anonymous and free.</p>
        </div>

        <div class="features">
            <div class="feature">🚨 Crisis Support</div>
            <div class="feature">💔 Emotional Support</div>
            <div class="feature">🌉 Community Connection</div>
            <div class="feature">🔒 100% Anonymous</div>
        </div>

        <div class="buttons">
            <button class="btn btn-primary" onclick="openApp()">Open Bridge App</button>
            <button class="btn btn-secondary" onclick="shareApp()">Share App</button>
        </div>

        <button class="btn download-btn" onclick="downloadQRCode()">Download QR Code</button>
    </div>

    <script>
        // Your Bridge App URL
        const APP_URL = 'https://lhmisme420.github.io/Bridge-App/';
        
        // Generate QR Code
        function generateQRCode() {
            const qrcodeContainer = document.getElementById('qrcode');
            
            QRCode.toCanvas(qrcodeContainer, APP_URL, {
                width: 200,
                margin: 2,
                color: {
                    dark: '#764ba2',
                    light: '#ffffff'
                }
            }, function(error) {
                if (error) {
                    console.error('QR Code generation failed:', error);
                    qrcodeContainer.innerHTML = `
                        <div style="padding: 2rem; text-align: center; color: #666;">
                            <p>⚠️ QR Code generation failed</p>
                            <p>Please visit: ${APP_URL}</p>
                        </div>
                    `;
                }
            });
        }

        // Open Bridge App
        function openApp() {
            window.open(APP_URL, '_blank');
        }

        // Share App
        function shareApp() {
            const shareData = {
                title: 'Bridge to Healing - Crisis Support',
                text: 'Get immediate crisis support in 3 clicks. Anonymous, free, no signups required.',
                url: APP_URL
            };

            if (navigator.share) {
                navigator.share(shareData)
                    .then(() => console.log('Shared successfully'))
                    .catch(error => console.log('Error sharing:', error));
            } else {
                // Fallback: Copy to clipboard
                navigator.clipboard.writeText(APP_URL).then(() => {
                    alert('App URL copied to clipboard! 📋\n\nShare: ' + APP_URL);
                }).catch(() => {
                    prompt('Copy this URL to share:', APP_URL);
                });
            }
        }

        // Download QR Code
        function downloadQRCode() {
            const canvas = document.querySelector('#qrcode canvas');
            if (canvas) {
                const link = document.createElement('a');
                link.download = 'bridge-app-qrcode.png';
                link.href = canvas.toDataURL('image/png');
                link.click();
            } else {
                alert('Please wait for QR code to generate');
            }
        }

        // Initialize
        document.addEventListener('DOMContentLoaded', function() {
            generateQRCode();
            document.getElementById('urlDisplay').textContent = APP_URL;
        });

        // Service Worker for PWA capabilities (optional)
        if ('serviceWorker' in navigator) {
            navigator.serviceWorker.register('/sw.js')
                .then(registration => console.log('SW registered'))
                .catch(error => console.log('SW registration failed'));
        }
    </script>
</body>
</html>
