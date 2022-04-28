# CollectivOps.net Landing Page

## About

This is a static website built on [HUGO](https://gohugo.io/) built for use by CollectivOps. While this template and assets herein are free to use by anyone, we may in some cases need to make changes from our live site at https://www.collectivops.net/ in order to utilize non-free assets. Depending on the needs of the collective, we may update our licensing, governance model, or take the repository private at any time. Anticipated changes to licensing include:

- Trademarking of CollectivOps branding including images, logos, catchphrases, color schemes, and typesets.
- Moving to a license with an attribution clause.

## How to Contribute

### ToDo List:

#### Minimum Viable Product (in order)
- [X] Base Template
- [X] Readme
- [ ] Initial Theme Selection
- [ ] Theme Layout building (if applicable)
- [ ] Color Scheme updates
- [ ] Dummy Assets (Images, videos, icons, text)
- [ ] CollectivOps Images ( !!! Not to be in repository if licensed !!! )
- [ ] CollectivOps Text
- [ ] Contact Us iFrame/Form

#### Enhanced (in no particular order)

- [ ] CollectivOps Videos ( !!! Not to be in repository if licensed !!! )
- [ ] Theming / Branding tweaks
- [ ] Creation of our own theme not based on initial template.
- [ ] Extension into CollectivOps "profiles" - providing promotional pages for each member or team within CollectivOps
- [ ] More robust integration with RTF and associated entities (however that looks)

### Getting started:

#### Prerequisites:

| Prerequisite  | Link |
| --- | --- |
| Docker | https://docs.docker.com/get-docker/ |
| Docker Compose | https://docs.docker.com/compose/install/ |


This project should only require that docker and docker-compose be installed on your local workstation. If using Windows or MacOS, definitely use Docker Desktop to make this easier. Otherwise more steps are required.

#### Working with the site:

This is a HUGO template, as such most information on the structure of this repository can be found [here](https://gohugo.io/getting-started/directory-structure/).

Outside of this, we are making the following structural decisions:

- All Licensed resources should not be committed. Use dummy resources that are Free/unrestricted instead.
  - Licensed resources can be dealt with in the following ways:
    - Create a `proprietary` directory under `assets` and add `assets/proprietary/*` to your `.gitignore` file. Then update your templates to reference this image. 
    - Create a separate private repository or file share, naming all images identically to the dummy image names in this repository. Download and overwrite the files in `Dockerfile.prod`
- Theme modifications should only be done once we find a theme and _fork_ it before adding it as a submodule. 

Once a theme is created, we can then provide better instructions on what sections are supported by the theme, how to configure them, and how to enhance the theme.

#### Running the site locally:

Run:

```
docker-compose up -d
```

Then navigate in a browser to `http://localhost:1313` to see a live version of the site. In this mode, you can update the site code and it will automatically update if you refresh the browser. 

#### Deploying / Running in production mode:

##### Deploying:

Everything is dockerized, so deploying is as simple as pushing the image to your repository, then using your prefered provider to pull and host that image.

```
docker build -t collectivops:latest -f Dockerfile.prod .
docker tag collectivops:latest $REGISTRY_HOST:$REGISTRY_PORT/$REGISTRY/$PATH:latest
docker login --username $USER $REGISTRY_HOST:$REGISTRY_PORT
docker push --all-tags $REGISTRY_HOST:$REGISTRY_PORT/$REGISTRY/$PATH
```

##### Prod Mode

A quick way to test prod mode is to run the `docker-compose.prod.yml` file instead of the standard one, to do this:

```
docker-compose -f docker-compose.prod.yml up -d
```

This builds the site into static resources and installs them on an NGINX webserver/proxy container. This implementation is entirely static and should really only be used to verify compatibility with the webserver.


