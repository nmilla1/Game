# Game

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>The Right Brain Game</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Inter', sans-serif;
        }
    </style>
</head>
<body class="bg-gradient-to-r from-purple-400 to-blue-500 h-screen flex justify-center items-center p-4">
    <div class="bg-white rounded-lg shadow-xl p-8 w-full max-w-2xl text-center">
        <h1 class="text-2xl font-semibold text-gray-800 mb-6">Two Random Things</h1>
        <div id="word-display" class="flex justify-center items-center gap-4 mb-6">
            <div id="word1" class="bg-indigo-200 text-indigo-700 px-4 py-2 rounded-md text-lg font-medium shadow-md"></div>
            <div id="word2" class="bg-indigo-200 text-indigo-700 px-4 py-2 rounded-md text-lg font-medium shadow-md"></div>
        </div>
        <button id="new-words-button" class="bg-gradient-to-r from-pink-500 to-purple-600 hover:from-pink-600 hover:to-purple-700 text-white font-semibold rounded-full py-3 px-6 transition duration-300 ease-in-out shadow-md hover:shadow-lg focus:outline-none focus:ring-2 focus:ring-purple-400 focus:ring-offset-2">
            Get Two New Objects
        </button>

        <div id="response-section" class="mt-8">
            <label for="response-input" class="block text-gray-700 text-sm font-bold mb-2">
                What could you create with these two objects?
            </label>
            <textarea id="response-input" placeholder="Describe your creative idea here..." class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline rounded-md"></textarea>
            <div id="email-section" class="mt-6">
                <label for="email-input" class="block text-gray-700 text-sm font-bold mb-2">
                    Want to send your response to your email?
                </label>
                <input type="email" id="email-input" placeholder="Enter your email address" class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline rounded-md mb-4">
                <p id="email-disclaimer" class="text-gray-500 text-xs italic mb-4">
                    We will only use your email to send you this response.
                </p>
                <button id="send-email-button" class="bg-green-500 hover:bg-green-700 text-white font-semibold rounded-full py-2 px-4 transition duration-300 ease-in-out shadow-md hover:shadow-lg focus:outline-none focus:ring-2 focus:ring-green-400 focus:ring-offset-2">
                    Send to Email
                </button>
                <p id="email-status" class="mt-2 text-gray-600"></p>
            </div>
        </div>
    </div>

    <script>
        const wordDisplay1 = document.getElementById('word1');
        const wordDisplay2 = document.getElementById('word2');
        const newWordsButton = document.getElementById('new-words-button');
        const responseInput = document.getElementById('response-input');
        const sendEmailButton = document.getElementById('send-email-button');
        const emailInput = document.getElementById('email-input');
        const emailStatus = document.getElementById('email-status');

        const words = ['Chair', 'Table', 'Lamp', 'Book', 'Computer', 'Phone', 'Pen', 'Paper', 'Car', 'Bike', 'Tree', 'Flower', 'Sun', 'Moon', 'Star', 'Cloud', 'Water', 'Fire', 'Food', 'Drink', 'Hat', 'Shoes', 'Shirt', 'Pants', 'House', 'Building', 'Bridge', 'Road', 'City', 'Country', 'World', 'Planet', 'Space', 'Time', 'Music', 'Art', 'Love', 'Friendship', 'Happiness', 'Sadness', 'Anger', 'Fear', 'Courage', 'Hope', 'Dream', 'Memory', 'Idea', 'Question', 'Answer', 'Beginning', 'End'];

        function getRandomWord() {
            return words[Math.floor(Math.random() * words.length)];
        }

        function displayRandomWords() {
            const word1 = getRandomWord();
            const word2 = getRandomWord();
            wordDisplay1.textContent = word1;
            wordDisplay2.textContent = word2;
            responseInput.value = ''; // Clear previous response
            emailStatus.textContent = ''; // Clear previous email status
            sendEmailButton.disabled = false; // Re-enable the email button
            sendEmailButton.classList.remove('bg-gray-400', 'cursor-not-allowed'); // Restore button style
            sendEmailButton.classList.add('bg-green-500', 'hover:bg-green-700');
        }

        newWordsButton.addEventListener('click', displayRandomWords);

        sendEmailButton.addEventListener('click', () => {
            const response = responseInput.value;
            const email = emailInput.value;

            if (!response) {
                emailStatus.textContent = "Please enter your creative idea.";
                return;
            }

            if (!email) {
                emailStatus.textContent = "Please enter your email address.";
                return;
            }

            if (!isValidEmail(email)) {
                emailStatus.textContent = "Invalid email address.";
                return;
            }

            // Disable the button and change its appearance to indicate processing
            sendEmailButton.disabled = true;
            sendEmailButton.textContent = "Sending...";
            sendEmailButton.classList.remove('bg-green-500', 'hover:bg-green-700');
            sendEmailButton.classList.add('bg-gray-400', 'cursor-not-allowed');

            // Simulate sending the email (replace with actual email sending logic)
            setTimeout(() => {
                emailStatus.textContent = "Response sent to " + email + "!";
                sendEmailButton.textContent = "Send to Email"; // Restore button text
                // Re-enable the button after the simulation is complete
                sendEmailButton.disabled = false;
                sendEmailButton.classList.remove('bg-gray-400', 'cursor-not-allowed'); // Restore button style
                sendEmailButton.classList.add('bg-green-500', 'hover:bg-green-700');
            }, 2000); // Simulate a 2-second delay
        });

        function isValidEmail(email) {
            // Basic email validation (you can use a more robust library)
            return /^[\w-\.]+@([\w-]+\.)+[\w-]{2,4}$/.test(email);
        }

        displayRandomWords(); // Initial display of words

    </script>
</body>
</html>
