## Despliegue Automatizado Utilizando Oracle Linux Automation Platform (OLAM) 

### Requerimientos:

- Cuenta de Oracle Cloud Infrastructure(test gratuito https://www.oracle.com/cloud/free/)
- Cuenta de Github (https://github.com/signup?ref_cta=Sign+up&ref_loc=header+logged+out&ref_page=%2F&source=header-home)

### ¿Qué vamos a hacer?

- Clonar repositorio Github
- Configurar OLAM
- Crear Credenciales en OLAM
- Crear Proyecto en OLAM
- Crear Templates en OLAM
- Crear Workflow en OLAM
- Crear Instancia de autonomous Database
- Crear un VCN con Subnet y Security List
- Crear Container Registry 
- Despliegue de aplicación en Container Instance 


### Paso a Paso

0. Crear Cuenta en git, usuar correo empresarial o personal (github.com)


https://user-images.githubusercontent.com/14284928/219779574-ad656998-a63d-402a-87cd-b9658c84e401.mov




1. Crear Repositorio Git y nombrar como tu empresa
**EJEMPLO: Si mi empresa se llama Empresa Jovial nombrar el nuevo repositorio git como empresajovial**


https://user-images.githubusercontent.com/14284928/220199906-8b80092a-e499-4835-8cce-e50c853be836.mov



2. Clonar el **siguiente repositorio Git  https://github.com/whiplash0104/Race-to-the-Cloud-app.git**

**NO COPIAR ESTE REPOSITORIO QUE TIENE LA DOCUMENTACIÓN, ES ESTE: https://github.com/whiplash0104/Race-to-the-Cloud-app.git**


https://user-images.githubusercontent.com/14284928/220199927-1c5220ba-95b4-4749-a14c-174fe4526a76.mov


2.1 Para validar que el repositorio fue clonado de forma correcta, una vez que finalice el proceso, entrar y dentro deberían tener 3 archivos:
- Dockerfile
- main.py
- requirements.txt

Si estos archivos no están se clonó un repositorio distinto y errado.

![image](https://user-images.githubusercontent.com/14284928/220200117-1a4061ce-2303-47af-9f5e-7e1de3537aa5.png)


3. Crear compartment llamado **RaceToCloud**

```
Menu > Identity & Security > Compartmente > New Compartment
```


https://user-images.githubusercontent.com/14284928/217977014-8c324c4f-0c7b-4781-8e6b-de335c80605d.mov




4. Login Dentro de OLAM en base a URL, usuario y contraseña entregada. **Es un acceso por empresa**


https://user-images.githubusercontent.com/14284928/217977128-936480e4-6dd3-44f1-afe5-5c5ec1326d8d.mov



### Validaciones Previas

Cada usuario debe tener creados los siguientes templates:
  - 01 - Crea ADB
  - 02 - Crea VCN 
  - 03 - Crea Registry 
  - 04 - Build Container Image 
  - 05 - Crea Instancia 
  - 06 - Elimina Container Instance NOMBREEMPRESA 
  - 07 - Elimina Registry NOMBREEMPRESA
  - 08 - Elimina VCN NOMBREEMPRESA
  - 09 - Elimina ADB NOMBREEMPRESA
  - NOMBREEMPRESA - WF Completo
  - NOMBREEMPRESA - WF Elimina Todo

![image](https://user-images.githubusercontent.com/14284928/219827568-13004994-5fa3-4c4d-b518-69c2ba5dbcd6.png)



5. Crear Credencial OCI, esta permite la íntegración entre OLAM y OCI
NOMBREMPRESA: es el nombre de cada empresa, no usar espacios ej: **si mi empresa se llama "Empresa Jovial" usar el nombre "EmpresaJovial"**

```
Menu > Accesos > Credenciales > Añadir

Nombre: Credencial OCI *NOMBREEMPRESA*
Organización: Selecionar la organización que corresponde a la empresa
```

https://user-images.githubusercontent.com/14284928/219782010-192d2a87-2cb6-4cb9-a1a3-d7362ad8ad60.mov



6. Una vez creada la credencial OCI ir al submenu Planillas:

```
Menu > Recursos > Planillas
```

Se encontrarán con las plantillas quue se utilizarán creadas

![image](https://user-images.githubusercontent.com/14284928/219783093-8d87e1e6-b63b-4ecb-bf74-86a23355efa6.png)



7. Dentro de Planilla (Templates) se encontrarán con uno llamado *NOMBREEMPRESA - WF Completo*, a este workflow se le deben agregar los templates a utilizar y la credencial de OCI recién creada


Abrir NOMBREEMPRESA - WF Completo 
Ir a la pestaña Visualizador
![image](https://user-images.githubusercontent.com/14284928/219784197-1da5d7c3-c38c-4b5c-821c-0a65958f4841.png)

Hacer click en el botón verde Iniciar
![image](https://user-images.githubusercontent.com/14284928/219784373-e37da084-7fbd-4009-9585-5b3acccc50c6.png)

Selecionar el Template *01. Crea ADB*  y click en Siguiente
![image](https://user-images.githubusercontent.com/14284928/219827358-4cc74e23-7459-4489-891f-c6dc5ba0c5b6.png)

En el grupo Credencial ir a la categoría Oracle Cloud Infrastructure, y selecionar la credencial de OCI creada en pasos anteriores. Una vez selecionada click en Siguiente


<img width="636" alt="image" src="https://user-images.githubusercontent.com/14284928/219827399-9221c847-deea-47ef-a406-2ef7b952b708.png">

NO HACER NINGÚN CAMBIO EN OTRAS CREDENCIALES y click en guardar

El workflow debió cambiar a algo similar a la imágen
![image](https://user-images.githubusercontent.com/14284928/219784989-34bf61f4-217d-4267-8686-7eb26436698a.png)

Pasar el mouse sobre el nombre de la planilla agregada y hacer click en el símbolo + para agregar el siguiente template
<img width="745" alt="image" src="https://user-images.githubusercontent.com/14284928/219785222-10ae741d-8f7c-4f7f-b1ea-955a43f2b438.png">

Hacer lo mismo para los todos los template en el sioguiente orden:

  1. 01 - Crea ADB
  2. 02 - Crea VCN 
  3. 03 - Crea Registry 
  4. 04 - Build Container Image 
  5. 05 - Crea Instancia 



https://user-images.githubusercontent.com/14284928/219827225-593d0e73-30a9-4963-b7a9-0bb0680d6e74.mov



8. Una vez creado el Workflow Ejecutarlo haciendo click en el botón Ejecutar

**IMPORTANTE**

```
Llenar los campos
Nombre Empresa          NombreEmpresa sin espacios
Compartment OCID
User OCID
Usuario OCI             Ejemplo: /oracleidentitycloudservice/USUARIO
URL Registry            Sin https://... ejemplo, si el registry es https://scl.ocir.io solo dejar scl.ocir.io
Token 
URL Git                 Repositorio clonado por uds, debe ser público
Nombre Repositorio      Definido por uds
Namespace Repository
```

![image](https://user-images.githubusercontent.com/14284928/219785666-3b417e2f-cb60-4cdc-aeef-9a72a607f1f5.png)



https://user-images.githubusercontent.com/14284928/219827439-e4f8c53b-2b33-48a6-9add-30e2d2b7fe1a.mov



9. Para probar la correcta ejecución del workflow ir a cloud.oracle.com > Menú Principal > Developer Service > Container Instances
![image](https://user-images.githubusercontent.com/14284928/219786328-25193514-173a-4586-8bfe-e26b12a084f5.png)
Dentro del compartment **RaceToCloud** creado recientemente ir a instancia llamada **GP-Instance** y dentro de este buscar la ip pública, 
abrir una nueva pestaña en el navegador, pegar la ip y asignar el puerto 8080



https://user-images.githubusercontent.com/14284928/219827446-639a602f-6729-456b-bc4a-e627b312d0ce.mov




10. Una vez validado el funcionamiento de la instancia, dentro de planillas editar el Workflow de eliminación y de la misma forma que en el punto 7, crear el workflow
Usar el siguiente orden:

  1.  06 - Elimina Container Instance NOMBREEMPRESA 
  2.  07 - Elimina Registry NOMBREEMPRESA
  3.  08 - Elimina VCN NOMBREEMPRESA
  4.  09 - Elimina ADB NOMBREEMPRESA



https://user-images.githubusercontent.com/14284928/219827454-8aab05ea-753e-4e95-acde-67827d8d0372.mov



11. Para validar que todo fuera eliminado se debe revidar VCN, ADB, Registry y Container Instance


https://user-images.githubusercontent.com/14284928/219827500-38c9a17e-f6f4-4026-aa59-889c1c7df781.mov

