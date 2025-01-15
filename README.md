# Assignment: Creating Interactive Elements and Form Validation

## Objective:
Build a functional webpage that incorporates event handling, interactive elements, and form validation using JavaScript.

## Requirements:

Interactive Button with onclick:

Add a button that toggles the background color of the webpage between two colors.
Slider with Real-Time Feedback (oninput):

Add a slider that adjusts the size of a paragraph text dynamically.
Modal with Event Listeners:

Create a modal that displays when a button is clicked and hides when the user clicks a close button.

## Form with Validation:

Include a form with the following fields:
Name (required, minimum 3 characters).
Email (valid email format).
Password (minimum 8 characters, at least one uppercase letter and one number).
Display error messages if validation fails.
Prevent form submission if there are errors.
Bonus (Optional):

Add a dropdown menu that displays a custom message when the selected option changes (onchange).

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Interactive Elements and Form Validation</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <h1>Interactive Webpage</h1>

  <!-- Interactive Button -->
  <button id="toggleButton">Toggle Background Color</button>

  <!-- Slider with Real-Time Feedback -->
  <label for="textSizeSlider">Adjust Text Size:</label>
  <input type="range" id="textSizeSlider" min="10" max="50" value="16">
  <p id="textPreview">This text will change size based on the slider.</p>

  <!-- Modal -->
  <button id="openModalButton">Open Modal</button>
  <div id="modal" class="modal">
    <div class="modal-content">
      <span id="closeModalButton" class="close">&times;</span>
      <p>This is a modal!</p>
    </div>
  </div>

  <!-- Form with Validation -->
  <form id="myForm">
    <label for="name">Name (min 3 characters):</label>
    <input type="text" id="name" name="name" required>
    <span id="nameError" class="error"></span><br>

    <label for="email">Email:</label>
    <input type="email" id="email" name="email" required>
    <span id="emailError" class="error"></span><br>

    <label for="password">Password (min 8 characters, one uppercase and one number):</label>
    <input type="password" id="password" name="password" required>
    <span id="passwordError" class="error"></span><br>

    <button type="submit">Submit</button>
  </form>

  <!-- Bonus Dropdown Menu -->
  <label for="messageSelect">Choose a message:</label>
  <select id="messageSelect">
    <option value="">Select...</option>
    <option value="Message 1">Message 1</option>
    <option value="Message 2">Message 2</option>
    <option value="Message 3">Message 3</option>
  </select>
  <p id="messageDisplay"></p>

  <script src="script.js"></script>
</body>
</html>

body {
  font-family: Arial, sans-serif;
}

button {
  margin: 10px;
}

#textPreview {
  font-size: 16px;
}

.modal {
  display: none;
  position: fixed;
  z-index: 1;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
}

.modal-content {
  background-color: white;
  margin: 15% auto;
  padding: 20px;
  width: 80%;
  max-width: 300px;
}

.close {
  color: #aaa;
  float: right;
  font-size: 28px;
  font-weight: bold;
}

.close:hover,
.close:focus {
  color: black;
  text-decoration: none;
  cursor: pointer;
}

.error {
  color: red;
  font-size: 12px;
}


// Toggle Background Color
document.getElementById('toggleButton').addEventListener('click', function () {
  document.body.style.backgroundColor = document.body.style.backgroundColor === 'lightblue' ? 'white' : 'lightblue';
});

// Slider with Real-Time Feedback
document.getElementById('textSizeSlider').addEventListener('input', function () {
  const size = this.value;
  document.getElementById('textPreview').style.fontSize = `${size}px`;
});

// Modal with Event Listeners
document.getElementById('openModalButton').addEventListener('click', function () {
  document.getElementById('modal').style.display = 'block';
});

document.getElementById('closeModalButton').addEventListener('click', function () {
  document.getElementById('modal').style.display = 'none';
});

// Form Validation
document.getElementById('myForm').addEventListener('submit', function (event) {
  event.preventDefault();

  // Clear previous error messages
  document.getElementById('nameError').textContent = '';
  document.getElementById('emailError').textContent = '';
  document.getElementById('passwordError').textContent = '';

  let isValid = true;

  // Name validation
  const name = document.getElementById('name').value;
  if (name.length < 3) {
    document.getElementById('nameError').textContent = 'Name must be at least 3 characters.';
    isValid = false;
  }

  // Email validation
  const email = document.getElementById('email').value;
  const emailPattern = /^[a-zA-Z0-9._-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$/;
  if (!emailPattern.test(email)) {
    document.getElementById('emailError').textContent = 'Please enter a valid email address.';
    isValid = false;
  }

  // Password validation
  const password = document.getElementById('password').value;
  const passwordPattern = /^(?=.*[A-Z])(?=.*\d).{8,}$/;
  if (!passwordPattern.test(password)) {
    document.getElementById('passwordError').textContent = 'Password must be at least 8 characters, with one uppercase letter and one number.';
    isValid = false;
  }

  // Submit form if valid
  if (isValid) {
    alert('Form submitted successfully!');
    // Normally, here you would submit the form using AJAX or regular form submission
  }
});

// Bonus: Dropdown Menu Event
document.getElementById('messageSelect').addEventListener('change', function () {
  const message = this.value;
  document.getElementById('messageDisplay').textContent = message ? `You selected: ${message}` : '';
});


