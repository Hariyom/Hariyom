<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>OTP Verification</title>
  <style>
    body {
      background-color: #0f172a;
      color: #fff;
      font-family: Arial, sans-serif;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      height: 100vh;
      margin: 0;
    }

    .icon {
      font-size: 60px;
      margin-bottom: 20px;
    }

    h2 {
      margin: 0;
    }

    p {
      color: #ccc;
      margin-bottom: 30px;
    }

    .otp-container {
      display: flex;
      gap: 10px;
    }

    .otp-input {
      width: 50px;
      height: 50px;
      font-size: 24px;
      text-align: center;
      border-radius: 10px;
      border: 2px solid #475569;
      background-color: #1e293b;
      color: #fff;
    }

    .otp-input:focus {
      outline: none;
      border-color: #3b82f6;
    }

    .keypad {
      margin-top: 30px;
      display: grid;
      grid-template-columns: repeat(3, 80px);
      gap: 10px;
    }

    .key {
      background-color: #1e293b;
      border: none;
      color: #fff;
      font-size: 24px;
      border-radius: 10px;
      padding: 20px 0;
      cursor: pointer;
    }

    .key:active {
      background-color: #334155;
    }
  </style>
</head>
<body>

  <div class="icon">📲</div>
  <h2>Enter code</h2>
  <p>We've sent an SMS with an activation code to your phone +91 6396488248.</p>

  <div class="otp-container">
    <input type="text" maxlength="1" class="otp-input" />
    <input type="text" maxlength="1" class="otp-input" />
    <input type="text" maxlength="1" class="otp-input" />
    <input type="text" maxlength="1" class="otp-input" />
    <input type="text" maxlength="1" class="otp-input" />
    <input type="text" maxlength="1" class="otp-input" />
  </div>

  <div class="keypad" id="keypad">
    <!-- Keys will be injected here -->
  </div>

  <script>
    const inputs = document.querySelectorAll('.otp-input');
    inputs[0].focus();

    inputs.forEach((input, index) => {
      input.addEventListener('input', () => {
        if (input.value && index < inputs.length - 1) {
          inputs[index + 1].focus();
        }
      });

      input.addEventListener('keydown', (e) => {
        if (e.key === 'Backspace' && !input.value && index > 0) {
          inputs[index - 1].focus();
        }
      });
    });

    // Virtual Keypad
    const keypad = document.getElementById('keypad');
    const keys = ['1','2','3','4','5','6','7','8','9','0','⌫'];

    keys.forEach(key => {
      const button = document.createElement('button');
      button.className = 'key';
      button.textContent = key;
      button.onclick = () => {
        const current = document.activeElement;
        const isInput = current.classList.contains('otp-input');

        if (key === '⌫') {
          if (isInput && current.value === '' && current.previousElementSibling) {
            current.previousElementSibling.focus();
            current.previousElementSibling.value = '';
          } else if (isInput) {
            current.value = '';
          }
        } else {
          if (isInput) {
            current.value = key;
            const next = current.nextElementSibling;
            if (next && next.classList.contains('otp-input')) {
              next.focus();
            }
          }
        }
      };
      keypad.appendChild(button);
    });
  </script>
</body>
</html>