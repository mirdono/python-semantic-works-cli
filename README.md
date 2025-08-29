# python-semantic-works-cli

Provides a base docker image to be used in [mu cli](https://github.com/mu-semtech/mu-cli) scripts. 
The main benefit over using the base python image is not having to install the dependencies each time the script is ran. See the [requirements](requirements.txt) file for which dependencies are installed.


## Usage for project scripts

Add the simple script store to your `docker-compose.yml` file:

```yaml

  project-scripts:
    image: semtech/simple-script-store:1.0.0
    volumes:
      - ./scripts/:/app/scripts/
    restart: "no"
```

Under `./scripts/config.json` use this image as your basis:

```json
{
  "version": "0.1",
  "scripts": [
    {
      "documentation": {
        "command": "example-command",
        "description": "Description for example script",
        "arguments": []
      },
      "environment": {
        "image": "mirdono/python-semantic-works-cli",
        "interactive": true,
        "script": "example/example.py",
        "join_networks": true
      },
      "mounts": {
        "app": "/project/"
      }
    }
  ]
}
```

