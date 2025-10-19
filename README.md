<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Taskitos</title>
    <meta name="description" content="Os melhores scripts e bots para Sala do Futuro e CMSP. Automatizar tarefas, grátis e rápido!">

    <!-- Estilos -->
    <link rel="stylesheet" href="https://taskitos.cupiditys.lol/styles.css?v=83">
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <link rel="icon" href="favicon.png">

    <style>
        /* ======== ANIMAÇÃO DO TÍTULO ======== */
        .logo h1 {
            display: inline-block;
            animation: kickAndEase 0.8s ease-in-out;
        }

        @keyframes kickAndEase {
            0% {
                transform: translateY(0) scale(1);
                opacity: 0;
            }
            25% {
                transform: translateY(-10px) scale(1.05);
                opacity: 1;
            }
            50% {
                transform: translateY(5px) scale(0.98);
            }
            75% {
                transform: translateY(-3px) scale(1.02);
            }
            100% {
                transform: translateY(0) scale(1);
            }
        }

        /* ======== RODAPÉ MINÚSCULO ======== */
        .footer {
            text-transform: lowercase;
        }
    </style>

    <!-- Scripts externos -->
    <script src="https://js.sentry-cdn.com/8d38ce047555b74bc9ae8c98ff73bb3c.min.js" crossorigin="anonymous"></script>
    <script async defer src="https://cdn.jsdelivr.net/gh/altcha-org/altcha/dist_i18n/pt-br.min.js" type="module"></script>
    <script async defer src="https://cdn.jsdelivr.net/npm/altcha@latest/dist/altcha.min.js" type="module"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/pako/2.1.0/pako.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/altcha@latest/dist/altcha.min.js"></script>
    <script src="shared-auth.js?v=87"></script>
    <script src="index.js?v=6"></script>
</head>

<body>
    <div class="container">
        <header class="header">
            <div class="logo">
                <h1 data-text="Taskitos">Taskitos</h1>
                <p class="subtitle">para sala do futuro e cmsp!</p>
            </div>
        </header>

        <section id="loginSection" class="section">
            <div class="login-container">
                <button type="button" id="quickLoginBtn" class="quick-login-btn" style="display: none;">
                    <span>Contas Salvas</span>
                    <span class="badge" id="accountCount">0</span>
                </button>
                <h2>Login</h2>
                <form id="loginForm" class="login-form">
                    <div class="input-group">
                        <label for="studentId">RA</label>
                        <div class="input-wrapper">
                            <input type="text" id="studentId" placeholder="RA + dígito + sp | ex: 123456790sp" required>
                            <button type="button" id="clearStudentId" class="clear-btn hidden">×</button>
                        </div>
                    </div>
                    
                    <div class="input-group">
                        <label for="password">Senha</label>
                        <div class="input-wrapper">
                            <input type="password" id="password" placeholder="Senha" required>
                            <button type="button" id="togglePassword" class="toggle-btn">👁</button>
                            <button type="button" id="clearPassword" class="clear-btn hidden">×</button>
                        </div>
                    </div>

                    <!-- Altcha CAPTCHA Widget -->
                    <div class="input-group">
                        <altcha-widget 
                            challengeurl="/api/altcha/challenge"
                            auto="onfocus"
                            hidefooter="true"
                            hidelogo="true"
                            language="pt-BR"
                            expire="120000">
                        </altcha-widget>
                    </div>

                    <div class="button-group">
                        <button type="button" id="loginNormal" class="btn btn-secondary">Atividades Pendentes</button>
                        <button type="button" id="loginOverdue" class="btn btn-secondary">Atividades Expiradas</button>
                    </div>
                </form>
            </div>
        </section>
    </div>

    <!-- Modais -->
    <div id="activityModal" class="modal hidden"> ... </div>
    <div id="progressOverlay" class="overlay hidden"> ... </div>
    <div id="notificationContainer" class="notification-container"></div>
    <div id="discordModal" class="modal hidden"> ... </div>

    <footer class="footer">
        entre no nosso servidor do discord
        <br><a href="https://discord.gg/platformdestroyer">platform destroyer - discord</a>
        <br>feito por cupiditys
        <br>"taskitos" nome por prongsfav
        <br>baseado em doritus
        <br>créditos: enzo mereles / talls
    </footer>

    <!-- Scripts adicionais -->
    <script>
        function enforceMinMax(input) {
            const min = parseInt(input.getAttribute('min'));
            const max = parseInt(input.getAttribute('max'));
            let value = parseInt(input.value);
            if (isNaN(value)) input.value = min;
            else if (value < min) input.value = min;
            else if (value > max) input.value = max;
        }

        document.addEventListener('DOMContentLoaded', function() {
            const numberInputs = document.querySelectorAll('input[type="number"]');
            numberInputs.forEach(input => {
                input.addEventListener('input', function() { enforceMinMax(this); });
                input.addEventListener('blur', function() { enforceMinMax(this); });
                input.addEventListener('keydown', function(e) {
                    const allowedKeys = [8, 9, 27, 13, 46, 37, 38, 39, 40];
                    const isNumber = (e.keyCode >= 48 && e.keyCode <= 57) || (e.keyCode >= 96 && e.keyCode <= 105);
                    if (!allowedKeys.includes(e.keyCode) && !isNumber && !e.ctrlKey) e.preventDefault();
                });
            });
        });
    </script>
</body>
</html>
