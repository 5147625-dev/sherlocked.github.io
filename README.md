# sherlocked.github.io

<!DOCTYPE html>
<html lang="cs">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Caesarova šifra</title>

    <style>
        * {
            box-sizing: border-box;
        }

        body {
            margin: 0;
            padding: 40px 20px;
            font-family: Arial, sans-serif;
            background: #151923;
            color: white;
        }

        .container {
            max-width: 650px;
            margin: 50px auto;
            padding: 35px;
            background: #222938;
            border-radius: 15px;
            box-shadow: 0 5px 25px rgba(0,0,0,0.3);
        }

        h1 {
            text-align: center;
            color: #61a5ff;
        }

        p {
            text-align: center;
            color: #b8c2d1;
        }

        label {
            display: block;
            margin-top: 25px;
            margin-bottom: 10px;
            font-weight: bold;
        }

        textarea {
            width: 100%;
            min-height: 120px;
            padding: 15px;
            border: 2px solid #3b4659;
            border-radius: 8px;
            background: #151923;
            color: white;
            font-size: 16px;
            resize: vertical;
        }

        textarea:focus {
            outline: none;
            border-color: #61a5ff;
        }

        .output {
            background: #192f40;
        }

        button {
            width: 100%;
            margin-top: 20px;
            padding: 14px;
            border: none;
            border-radius: 8px;
            background: #3285ed;
            color: white;
            font-size: 16px;
            font-weight: bold;
            cursor: pointer;
        }

        button:hover {
            background: #1c6dcc;
        }

        .note {
            margin-top: 20px;
            font-size: 13px;
        }
    </style>
</head>

<body>

    <div class="container">

        <h1>Caesarova šifra</h1>

        <p>
            Zašifruj svůj text pomocí Caesarovy šifry.
        </p>

        <label for="inputText">
            Text k zašifrování:
        </label>

        <textarea
            id="inputText"
            placeholder="Napiš text, který chceš zašifrovat..."
        ></textarea>

        <button onclick="encryptText()">
            Zašifrovat text
        </button>

        <label for="outputText">
            Zašifrovaný text:
        </label>

        <textarea
            id="outputText"
            class="output"
            placeholder="Zde se zobrazí zašifrovaný text..."
            readonly
        ></textarea>

        <button onclick="copyText()">
            Kopírovat zašifrovaný text
        </button>

        <p class="note">
            Používáme anglickou abecedu ABCDEFGHIJKLMNOPQRSTUVWXYZ.
            Posun šifry je vždy o jedno písmeno.
        </p>

    </div>

    <script>

        function encryptText() {

            const text = document.getElementById("inputText").value;

            const alphabet = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";

            let encryptedText = "";

            for (let i = 0; i < text.length; i++) {

                const character = text[i];

                const upperCharacter = character.toUpperCase();

                const position = alphabet.indexOf(upperCharacter);

                if (position !== -1) {

                    const newPosition = (position + 1) % 26;

                    let newCharacter = alphabet[newPosition];

                    // Zachování malých a velkých písmen
                    if (character === character.toLowerCase()) {
                        newCharacter = newCharacter.toLowerCase();
                    }

                    encryptedText += newCharacter;

                } else {

                    // Mezery, čísla a interpunkce zůstávají stejné
                    encryptedText += character;

                }
            }

            document.getElementById("outputText").value = encryptedText;
        }

        function copyText() {

            const output = document.getElementById("outputText");

            navigator.clipboard.writeText(output.value)
                .then(() => {
                    alert("Text byl zkopírován!");
                })
                .catch(() => {
                    alert("Kopírování se nepodařilo.");
                });

        }

    </script>

</body>
</html>
