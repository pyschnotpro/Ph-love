# Ph-love<!index.html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Free Casino Demo</title>
    <!-- Free CSS Framework (Bulma) -->
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bulma@0.9.4/css/bulma.min.css">
    <!-- Font Awesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
    <style>
        .hero { background: linear-gradient(45deg, #1a1a2e, #16213e); }
        .game-card { transition: transform 0.3s; cursor: pointer; }
        .game-card:hover { transform: scale(1.05); }
        footer { margin-top: 50px; }
    </style>
</head>
<body>
    <!-- Header -->
    <section class="hero is-medium">
        <div class="hero-body">
            <div class="container has-text-centered">
                <h1 class="title has-text-white"><i class="fas fa-coins"></i> Free Casino Demo</h1>
                <p class="subtitle has-text-light">Play fun games for free!</p>
                <!-- Guest Login Button -->
                <button class="button is-info" onclick="firebase.auth().signInAnonymously()">
                    <i class="fas fa-user-secret"></i> Play as Guest
                </button>
            </div>
        </div>
    </section>

    <!-- Games Grid -->
    <section class="section">
        <div class="container">
            <div class="columns is-multiline">
                <!-- Slot Machine -->
                <div class="column is-4">
                    <div class="game-card card">
                        <div class="card-content">
                            <h2 class="title is-5"><i class="fas fa-sliders-h"></i> Slots</h2>
                            <button class="button is-primary" onclick="spinSlots()">
                                <i class="fas fa-redo"></i> Spin!
                            </button>
                            <p id="slotsResult" class="mt-3 has-text-weight-bold"></p>
                        </div>
                    </div>
                </div>

                <!-- Dice Game -->
                <div class="column is-4">
                    <div class="game-card card">
                        <div class="card-content">
                            <h2 class="title is-5"><i class="fas fa-dice"></i> Dice Roll</h2>
                            <button class="button is-danger" onclick="rollDice()">
                                <i class="fas fa-dice"></i> Roll Dice
                            </button>
                            <p id="diceResult" class="mt-3 has-text-weight-bold"></p>
                        </div>
                    </div>
                </div>

                <!-- Test Payment Button -->
                <div class="column is-4">
                    <div class="game-card card">
                        <div class="card-content">
                            <h2 class="title is-5"><i class="fas fa-wallet"></i> Buy Chips</h2>
                            <button class="button is-success" id="checkout-button">
                                <i class="fas fa-credit-card"></i> Test Payment
                            </button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- Footer Disclaimer -->
    <footer class="footer has-background-dark has-text-light">
        <div class="content has-text-centered">
            <p>⚠️ This is a demo site. No real money is used.</p>
        </div>
    </footer>

    <!-- Firebase Auth -->
    <script src="https://www.gstatic.com/firebasejs/8.10.0/firebase-app.js"></script>
    <script src="https://www.gstatic.com/firebasejs/8.10.0/firebase-auth.js"></script>
    <!-- Stripe Payments -->
    <script src="https://js.stripe.com/v3/"></script>

    <!-- JavaScript Code -->
    <script>
        // Firebase Configuration (Replace with your keys!)
        const firebaseConfig = {
            apiKey: "YOUR_FIREBASE_API_KEY",
            authDomain: "YOUR_FIREBASE_AUTH_DOMAIN",
            projectId: "YOUR_FIREBASE_PROJECT_ID",
        };
        firebase.initializeApp(firebaseConfig);

        // Slot Machine Logic
        function spinSlots() {
            const symbols = ["🍒", "🍊", "🍋", "💰", "7️⃣"];
            const result = Array.from({ length: 3 }, () => symbols[Math.floor(Math.random() * symbols.length)]);
            document.getElementById("slotsResult").textContent = result.join(" | ");
        }

        // Dice Roll Logic
        function rollDice() {
            const dice = Math.floor(Math.random() * 6) + 1;
            document.getElementById("diceResult").textContent = `You rolled: ${dice}`;
        }

        // Stripe Test Payment (Replace with your key!)
        const stripe = Stripe('pk_test_YOUR_STRIPE_KEY');
        document.getElementById('checkout-button').addEventListener('click', () => {
            stripe.redirectToCheckout({ sessionId: 'TEST_SESSION_ID' });
        });
    </script>
</body>
</html>
