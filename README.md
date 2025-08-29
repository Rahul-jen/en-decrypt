<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>SecureCrypt - Data Encryption & Decryption Tool</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        body {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        .glass-effect {
            background: rgba(255, 255, 255, 0.15);
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.2);
            border-radius: 20px;
            box-shadow: 0 8px 32px rgba(0, 0, 0, 0.1);
        }
        
        .crypto-card {
            transition: all 0.3s ease;
            cursor: pointer;
        }
        
        .crypto-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 12px 24px rgba(0, 0, 0, 0.2);
        }
        
        .btn-primary {
            background: linear-gradient(45deg, #667eea, #764ba2);
            transition: all 0.3s ease;
        }
        
        .btn-primary:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 12px rgba(0, 0, 0, 0.2);
        }
        
        .result-box {
            min-height: 100px;
            word-break: break-all;
        }
        
        .security-indicator {
            transition: all 0.3s ease;
        }
        
        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.05); }
            100% { transform: scale(1); }
        }
        
        .pulse {
            animation: pulse 2s infinite;
        }
    </style>
</head>
<body class="min-h-screen flex items-center justify-center p-4">
    <div class="container mx-auto max-w-4xl">
        <!-- Header Section -->
        <header class="text-center mb-8">
            <div class="glass-effect p-6 mb-6">
                <h1 class="text-4xl md:text-5xl font-bold text-white mb-4">
                    <i class="fas fa-lock mr-3"></i>SecureCrypt
                </h1>
                <p class="text-lg text-white opacity-80">
                    Advanced AES-256 Encryption & Decryption Tool
                </p>
            </div>
            
            <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mb-8">
                <div class="crypto-card glass-effect p-6 text-center">
                    <i class="fas fa-key text-3xl text-green-400 mb-3"></i>
                    <h3 class="text-xl font-semibold text-white mb-2">Military Grade Encryption</h3>
                    <p class="text-white opacity-80">AES-256 bit encryption for maximum security</p>
                </div>
                <div class="crypto-card glass-effect p-6 text-center">
                    <i class="fas fa-shield-alt text-3xl text-blue-400 mb-3"></i>
                    <h3 class="text-xl font-semibold text-white mb-2">Real-time Processing</h3>
                    <p class="text-white opacity-80">Instant encryption and decryption results</p>
                </div>
            </div>
        </header>

        <!-- Main Encryption Interface -->
        <main class="glass-effect p-6 md:p-8">
            <!-- Input Section -->
            <div class="mb-6">
                <label class="block text-white text-sm font-bold mb-2" for="inputText">
                    <i class="fas fa-pencil-alt mr-2"></i>Input Text
                </label>
                <textarea 
                    id="inputText" 
                    class="w-full p-4 rounded-lg bg-white bg-opacity-90 border border-white border-opacity-30 focus:outline-none focus:ring-2 focus:ring-blue-400 resize-none"
                    rows="4" 
                    placeholder="Enter text to encrypt or ciphertext to decrypt..."
                ></textarea>
            </div>

            <!-- Key Input Section -->
            <div class="mb-6">
                <div class="flex items-center justify-between mb-2">
                    <label class="block text-white text-sm font-bold" for="encryptionKey">
                        <i class="fas fa-key mr-2"></i>Encryption Key
                    </label>
                    <button 
                        id="generateKeyBtn" 
                        class="text-xs text-blue-300 hover:text-blue-100 transition-colors"
                    >
                        <i class="fas fa-sync-alt mr-1"></i>Generate Random Key
                    </button>
                </div>
                <input 
                    type="password" 
                    id="encryptionKey" 
                    class="w-full p-4 rounded-lg bg-white bg-opacity-90 border border-white border-opacity-30 focus:outline-none focus:ring-2 focus:ring-blue-400"
                    placeholder="Enter your encryption key (minimum 8 characters)..."
                />
                <div class="flex items-center mt-2">
                    <span class="text-white text-xs mr-2">Key Strength:</span>
                    <div id="keyStrength" class="flex-1 h-2 bg-white bg-opacity-20 rounded-full">
                        <div id="strengthBar" class="h-full bg-red-400 rounded-full w-0 transition-all duration-300"></div>
                    </div>
                </div>
            </div>

            <!-- Action Buttons -->
            <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mb-6">
                <button 
                    id="encryptBtn" 
                    class="btn-primary text-white font-bold py-4 px-6 rounded-lg flex items-center justify-center"
                >
                    <i class="fas fa-lock mr-2"></i>Encrypt Data
                </button>
                <button 
                    id="decryptBtn" 
                    class="bg-white bg-opacity-20 text-white font-bold py-4 px-6 rounded-lg hover:bg-opacity-30 transition-all flex items-center justify-center"
                >
                    <i class="fas fa-unlock mr-2"></i>Decrypt Data
                </button>
            </div>

            <!-- Result Section -->
            <div class="mb-6">
                <label class="block text-white text-sm font-bold mb-2">
                    <i class="fas fa-file-alt mr-2"></i>Result
                </label>
                <div id="result" class="result-box w-full p-4 rounded-lg bg-white bg-opacity-10 border border-white border-opacity-20 text-white whitespace-pre-wrap">
                    <div class="flex items-center justify-center h-24 text-white opacity-50">
                        <i class="fas fa-arrow-down text-2xl mr-2"></i>
                        <span>Your encrypted or decrypted result will appear here</span>
                    </div>
                </div>
            </div>

            <!-- Action Buttons for Result -->
            <div class="flex flex-wrap gap-2">
                <button 
                    id="copyResultBtn" 
                    class="bg-white bg-opacity-20 text-white px-4 py-2 rounded-lg hover:bg-opacity-30 transition-all flex items-center"
                    disabled
                >
                    <i class="fas fa-copy mr-2"></i>Copy Result
                </button>
                <button 
                    id="clearAllBtn" 
                    class="bg-white bg-opacity-20 text-white px-4 py-2 rounded-lg hover:bg-opacity-30 transition-all flex items-center"
                >
                    <i class="fas fa-trash mr-2"></i>Clear All
                </button>
                <button 
                    id="downloadBtn" 
                    class="bg-white bg-opacity-20 text-white px-4 py-2 rounded-lg hover:bg-opacity-30 transition-all flex items-center"
                    disabled
                >
                    <i class="fas fa-download mr-2"></i>Download
                </button>
            </div>
        </main>

        <!-- Security Information -->
        <div class="glass-effect p-6 mt-6">
            <h3 class="text-xl font-semibold text-white mb-4 flex items-center">
                <i class="fas fa-info-circle mr-2"></i>Security Information
            </h3>
            <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                <div class="text-white text-sm">
                    <p class="mb-2"><i class="fas fa-check-circle text-green-400 mr-2"></i>AES-256 bit encryption</p>
                    <p class="mb-2"><i class="fas fa-check-circle text-green-400 mr-2"></i>Military-grade security</p>
                    <p class="mb-2"><i class="fas fa-check-circle text-green-400 mr-2"></i>Client-side processing</p>
                </div>
                <div class="text-white text-sm">
                    <p class="mb-2"><i class="fas fa-shield-alt text-blue-400 mr-2"></i>No data stored</p>
                    <p class="mb-2"><i class="fas fa-user-shield text-blue-400 mr-2"></i>Complete privacy</p>
                    <p class="mb-2"><i class="fas fa-bolt text-yellow-400 mr-2"></i>Real-time processing</p>
                </div>
            </div>
        </div>

        <!-- Hero Image -->
        <div class="mt-8 text-center">
            <img 
                src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/5ce4a2e0-4880-4c03-ae42-e1053c430ab2.png" 
                alt="Modern cybersecurity concept illustration showing digital lock and shield protecting data streams with glowing encryption symbols and secure network connections" 
                class="rounded-2xl mx-auto shadow-xl"
            />
        </div>
    </div>

    <script>
        // CryptoJS library for AES encryption (included via CDN)
        const script = document.createElement('script');
        script.src = 'https://cdnjs.cloudflare.com/ajax/libs/crypto-js/4.1.1/crypto-js.min.js';
        document.head.appendChild(script);

        script.onload = function() {
            // Initialize the application
            initializeApp();
        };

        function initializeApp() {
            const inputText = document.getElementById('inputText');
            const encryptionKey = document.getElementById('encryptionKey');
            const generateKeyBtn = document.getElementById('generateKeyBtn');
            const encryptBtn = document.getElementById('encryptBtn');
            const decryptBtn = document.getElementById('decryptBtn');
            const result = document.getElementById('result');
            const copyResultBtn = document.getElementById('copyResultBtn');
            const clearAllBtn = document.getElementById('clearAllBtn');
            const downloadBtn = document.getElementById('downloadBtn');
            const strengthBar = document.getElementById('strengthBar');

            // Generate random key
            generateKeyBtn.addEventListener('click', () => {
                const randomKey = generateRandomKey(32); // 32 characters = 256 bits
                encryptionKey.value = randomKey;
                updateKeyStrength(randomKey);
            });

            // Update key strength indicator
            encryptionKey.addEventListener('input', () => {
                updateKeyStrength(encryptionKey.value);
            });

            // Encrypt button click
            encryptBtn.addEventListener('click', () => {
                const text = inputText.value.trim();
                const key = encryptionKey.value.trim();

                if (!text) {
                    showNotification('Please enter text to encrypt', 'error');
                    return;
                }

                if (!key || key.length < 8) {
                    showNotification('Encryption key must be at least 8 characters', 'error');
                    return;
                }

                try {
                    const encrypted = encryptAES(text, key);
                    displayResult(encrypted, 'encrypted');
                    showNotification('Text encrypted successfully!', 'success');
                } catch (error) {
                    showNotification('Encryption failed: ' + error.message, 'error');
                }
            });

            // Decrypt button click
            decryptBtn.addEventListener('click', () => {
                const text = inputText.value.trim();
                const key = encryptionKey.value.trim();

                if (!text) {
                    showNotification('Please enter text to decrypt', 'error');
                    return;
                }

                if (!key) {
                    showNotification('Please enter the encryption key', 'error');
                    return;
                }

                try {
                    const decrypted = decryptAES(text, key);
                    displayResult(decrypted, 'decrypted');
                    showNotification('Text decrypted successfully!', 'success');
                } catch (error) {
                    showNotification('Decryption failed: Invalid key or ciphertext', 'error');
                }
            });

            // Copy result button
            copyResultBtn.addEventListener('click', () => {
                const resultText = result.textContent;
                navigator.clipboard.writeText(resultText).then(() => {
                    showNotification('Result copied to clipboard!', 'success');
                });
            });

            // Clear all button
            clearAllBtn.addEventListener('click', () => {
                inputText.value = '';
                encryptionKey.value = '';
                result.innerHTML = '<div class="flex items-center justify-center h-24 text-white opacity-50"><i class="fas fa-arrow-down text-2xl mr-2"></i><span>Your encrypted or decrypted result will appear here</span></div>';
                strengthBar.style.width = '0%';
                strengthBar.className = 'h-full bg-red-400 rounded-full transition-all duration-300';
                copyResultBtn.disabled = true;
                downloadBtn.disabled = true;
                showNotification('All fields cleared', 'info');
            });

            // Download button
            downloadBtn.addEventListener('click', () => {
                const resultText = result.textContent;
                const blob = new Blob([resultText], { type: 'text/plain' });
                const url = URL.createObjectURL(blob);
                const a = document.createElement('a');
                a.href = url;
                a.download = 'securecrypt_result.txt';
                document.body.appendChild(a);
                a.click();
                document.body.removeChild(a);
                URL.revokeObjectURL(url);
            });

            // AES Encryption function
            function encryptAES(text, key) {
                return CryptoJS.AES.encrypt(text, key).toString();
            }

            // AES Decryption function
            function decryptAES(ciphertext, key) {
                const bytes = CryptoJS.AES.decrypt(ciphertext, key);
                return bytes.toString(CryptoJS.enc.Utf8);
            }

            // Generate random key
            function generateRandomKey(length) {
                const chars = 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789!@#$%^&*()';
                let result = '';
                for (let i = 0; i < length; i++) {
                    result += chars.charAt(Math.floor(Math.floor(Math.random() * chars.length)));
                }
                return result;
            }

            // Update key strength indicator
            function updateKeyStrength(key) {
                let strength = 0;
                if (key.length >= 8) strength += 25;
                if (key.length >= 12) strength += 25;
                if (/[A-Z]/.test(key)) strength += 15;
                if (/[a-z]/.test(key)) strength += 15;
                if (/[0-9]/.test(key)) strength += 10;
                if (/[^A-Za-z0-9]/.test(key)) strength += 10;

                strengthBar.style.width = strength + '%';
                
                if (strength < 50) {
                    strengthBar.className = 'h-full bg-red-400 rounded-full transition-all duration-300';
                } else if (strength < 80) {
                    strengthBar.className = 'h-full bg-yellow-400 rounded-full transition-all duration-300';
                } else {
                    strengthBar.className = 'h-full bg-green-400 rounded-full transition-all duration-300';
                }
            }

            // Display result
            function displayResult(text, type) {
                result.innerHTML = `
                    <div class="mb-2 flex items-center justify-between">
                        <span class="text-sm font-semibold ${type === 'encrypted' ? 'text-green-400' : 'text-blue-400'}">
                            <i class="fas ${type === 'encrypted' ? 'fa-lock' : 'fa-unlock'} mr-2"></i>
                            ${type === 'encrypted' ? 'ENCRYPTED' : 'DECRYPTED'} TEXT
                        </span>
                        <span class="text-xs opacity-70">${new Date().toLocaleTimeString()}</span>
                    </div>
                    <div class="font-mono text-sm leading-relaxed">${text}</div>
                `;
                copyResultBtn.disabled = false;
                downloadBtn.disabled = false;
            }

            // Show notification
            function showNotification(message, type) {
                // Simple notification implementation
                const notification = document.createElement('div');
                notification.className = `fixed top-4 right-4 p-4 rounded-lg text-white font-semibold ${
                    type === 'error' ? 'bg-red-500' : 
                    type === 'success' ? 'bg-green-500' : 'bg-blue-500'
                } shadow-lg z-50`;
                notification.textContent = message;
                notification.style.transform = 'translateX(100%)';
                document.body.appendChild(notification);

                setTimeout(() => {
                    notification.style.transform = 'translateX(0)';
                }, 100);

                setTimeout(() => {
                    notification.style.transform = 'translateX(100%)';
                    setTimeout(() => {
                        document.body.removeChild(notification);
                    }, 300);
                }, 3000);
            }
        }
    </script>
</body>
</html>

