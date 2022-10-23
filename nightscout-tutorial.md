# Desplegar nightscout

## Introduccion
Con este asistente podremos desplegar la infraestructura necesaria para poder monitorizar con nuestro propio nightscout. 

Es posible que algunos de estos pasos requieran de algo de tiempo para finalizarse, por lo que hay que tener un poco de paciencia, de todas formas siempre podremos ver barras de estado que nos dará información.

Selecciona el proyecto de google cloud sobre el que desplegaremos la infraestructura.

<walkthrough-project-setup billing=true></walkthrough-project-setup>

## Configuración

Identificador del proyecto: <walkthrough-project-id/>

A continuación de manera asistida será necesario completar los siguiente pasos haciendo clic en <walkthrough-cloud-shell-icon></walkthrough-cloud-shell-icon> de cada uno de ellos y despues la tecla intro.

## Login

Debemos iniciar sesión con nuestro usuario
```sh  
gcloud auth login
```

**Ayuda**: Se puede ver el Flujo Login.

## Configuración proyecto

Debemos seleccionar el proyecto de google cloud sobre el que desplegar la infraestructura
```sh  
gcloud config set project <walkthrough-project-id/>
```

A continuación habilitaremos los apis necesarios
```sh  
gcloud services enable compute.googleapis.com deploymentmanager.googleapis.com  
```

## Desplegar máquina

Crear despliegue de máquina
```sh  
gcloud deployment-manager deployments create nighscout-deployment --template data/vm.jinja
```

Entrar dentro de la máquina
```sh
gcloud compute ssh nightscout-vm
```

Ejecutar la instalación de nightscout
```sh
curl https://raw.githubusercontent.com/jamorham/nightscout-vps/vps-1/bootstrap.sh | bash
```


## Felicidades

<walkthrough-conclusion-trophy></walkthrough-conclusion-trophy>

Ya cuentas con un servidor para realizar tu seguimiento con nightscout sobre Google Cloud.