# Desplegar nightscout

## Introduccion
### Español
Con este asistente podremos desplegar la infraestructura necesaria para poder monitorizar con nuestro propio nightscout. 

Es posible que algunos de estos pasos requieran de algo de tiempo para finalizarse, por lo que hay que tener un poco de paciencia, de todas formas siempre podremos ver barras de estado que nos dará información.

Selecciona el proyecto de google cloud sobre el que desplegaremos la infraestructura.

### English
With this wizard we will be able to deploy the necessary infrastructure to be able to monitor with our own nightscout.

It is possible that some of these steps require some time to complete, so you have to have a little patience, anyway we can always see status bars that will give us information.

Select the google cloud project on which we will deploy the infrastructure.

<walkthrough-project-setup billing=true></walkthrough-project-setup>

## Configuración/Setting

Identificador del proyecto/Project Id: <walkthrough-project-id/>

A continuación de manera asistida será necesario completar los siguiente pasos haciendo clic en <walkthrough-cloud-shell-icon></walkthrough-cloud-shell-icon> de cada uno de ellos y despues la tecla intro.

Next, in an assisted manner, it will be necessary to complete the following steps by clicking on <walkthrough-cloud-shell-icon></walkthrough-cloud-shell-icon> of each of them and then the enter key.

## Login

Debemos iniciar sesión con nuestro usuario

We must log in with our user

```sh  
gcloud auth login
```

**Ayuda**: Se puede ver el Flujo Login.

## Configuración proyecto/Project configuration

Debemos seleccionar el proyecto de google cloud sobre el que desplegar la infraestructura

We must select the google cloud project on which to deploy the infrastructure

```sh  
gcloud config set project <walkthrough-project-id/>
```

Configurar la zona por defecto 

Set the default zone

```sh
gcloud config set compute/zone us-central1-a
```

A continuación habilitaremos los apis necesarios
Next we will enable the necessary apis

```sh  
gcloud services enable compute.googleapis.com deploymentmanager.googleapis.com  
```

## Desplegar máquina/Deploy

Crear despliegue de máquina

Create machine deployment

```sh  
gcloud deployment-manager deployments create nighscout-deployment --template data/vm.jinja
```

## Instalación/Install

Entrar dentro de la máquina

Login in the VM
```sh
gcloud compute ssh nightscout-vm
```

Ejecutar la instalación de nightscout

Install nightscout
```sh
curl https://raw.githubusercontent.com/jamorham/nightscout-vps/vps-1/bootstrap.sh | bash
```


## Felicidades/Congratulations

<walkthrough-conclusion-trophy></walkthrough-conclusion-trophy>

Ya cuentas con un servidor para realizar tu seguimiento con nightscout sobre Google Cloud.

You already have a server to carry out your monitoring with nightscout on Google Cloud.

## Borrar proyecto/Delete Project

```sh
gcloud deployment-manager deployments delete nighscout-deployment
```
