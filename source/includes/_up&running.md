# Get edChain up and running

## Run edChain API server

* Move into the project directory: `cd edchain-api`

* Run `node app.js`

* You should see a message on the console saying *"connected to database"*. If you see any errors please take a look at the <a href="#debugging">debugging</a> section.

* Congrats! Your edChain-API is live and listening on **"YOUR_IP_ADDRESS:3000"**

## Run edChain videoScraper module

* Move into the project directory: `cd edchain-videoScraper/edchain-videoScraper`

* Run `gunicorn --bind 0.0.0.0:8000 wsgi`

* You should see a message on the console saying *"Listening at: http://0.0.0.0:8000"*. If you see any errors checkout the <a href="#debugging">debugging</a> section.

* Bravo! Your edChain-VideoScraper server is up and listening on port **8000**.

<aside class="warning">
	Make sure port <strong>8000</strong> is not in use before running the videoScraper module. You can use any other port but make sure you update the port number in edChain-api [TODO: Mention which file to change]
</aside>

## Run edChain android application

* Move into the project directory: `cd edchain-android`

* Run `react-native run-android`

* This command should get the app running on the simulator or a Physical device. If you see any errors checkout the <a href="#debugging">debugging</a> section.