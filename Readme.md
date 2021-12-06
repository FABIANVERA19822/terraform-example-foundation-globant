# Bitacora detallada instalacion gcp-terraform-Foundation-example-2.3 con  Terraform por Equipo GCP-Keralty-Itaka

**Autores :**             📅 **Fecha de Creacion : 4-12-2021**

 🧑🏻‍💻  **Fabian Vera        -  Cloud Engineer Sr  at Globant**   🇨🇴 ****

 🧑‍💻  **Gustavo Zocco  -  SysAdmin Engineer at Globant**  🇦🇷

 👨🏻‍💻 **Arturo Guaracha - Cloud Engineer at Globant**          🇲🇽 

 **Apoyos especiales :**

  🧑🏻‍🔧 **Daniel Burbano    - Cloud Engineer  at Globant**       🇨🇴 

  🧑🏻‍🔧 **Manuel Aller at Globant**  

## Recomendaciones de tecnologias usadas :

- [x]  [Cuenta en Google Cloud Platform](https://console.cloud.google.com/) con una Organizacion con dominio Propio
- [x]  [Google Cloud SDK version 319.0.0. o superior](https://cloud.google.com/sdk/docs/install)
- [x]  [Terraform version 0.13.7](https://releases.hashicorp.com/terraform/0.13.7/)
- [x]  Terraform Validator v0.40
- [x]  Git version 2.25.1 o superior
- [x]  Cualquier IDE de Desarollo con la que se sienta comodo, recomendamos **[Visual Studio Code](https://code.visualstudio.com/download)** con los siguientes plugins
- GitGraph
- Git Lens
- [x]  Terraform HCL
- [x]  Cualquier **Editor de Texto** con el que te sientas comodo recomendamos [Notepad ++](https://notepad-plus-plus.org/downloads/)
- [x]  **Sistemas Operativos** : Windows o Linux , recomendamos cualquiera con la que te sientas comodo, nuestro equipo trabajo muy bien bajo Linux Baremetal [Ubuntu 20.04.03 LTS](https://ubuntu.com/download/desktop), esto con el objetivo de que no se puedan llegar a romper los enlaces simbolicos basados en linux.

# **Prerrequisitos:**

- [x]  Por favor antes de iniciar, lea y comprenda la Guia de seguiridad de Google - Google Cloud Security Foundation Guide
- [x]  Su organizacion debera solicitar al equipo de Soporte el Aumento de su Quota de Projectos
- [x]  Para la Automatizacion de IaaC  y de Aplicaciones usaremos Terraform y Google Cloud Build como herrameinta de CI/CD  por lo tanto la API debera estar Habilitada.
- [x]  Asegurese de estar tener configurado debidamente su contexto de configuracion con el proyecto privote, la region, zona y usuario que ejecutara los scripts de Terraform e interactura con Google Cloud platform, use el comando: gcloud auth login
- [x]  Su Organizacion debera garantizar los siguientes Grupos  con sus respectivos permisos :

Aqui un ejemplo de asignacion de persmisos para usarlos via Google Cloud Shell y/o Bash Terminal Local de su IDE de desarollo preferido

- -member=group:gcp-organization-admins-fvera@gcpsandbox.cloud --role=roles/billing.admin
gcloud organizations add-iam-policy-binding 63734882150 \
--member=group:gcp-organization-admins-fvera@gcpsandbox.cloud --role=roles/billing.user
gcloud organizations add-iam-policy-binding 63734882150 \
--member=group:gcp-organization-admins-fvera@gcpsandbox.cloud --role=roles/cloudsupport.admin
gcloud organizations add-iam-policy-binding 63734882150 \
--member=group:gcp-organization-admins-fvera@gcpsandbox.cloud --role=roles/iam.organizationRoleAdmin
gcloud organizations add-iam-policy-binding 63734882150 \
--member=group:gcp-organization-admins-fvera@gcpsandbox.cloud --role=roles/orgpolicy.policyAdmin
gcloud organizations add-iam-policy-binding 63734882150 \
--member=group:gcp-organization-admins-fvera@gcpsandbox.cloud --role=roles/resourcemanager.folderAdmin
gcloud organizations add-iam-policy-binding 63734882150 \
--member=group:gcp-organization-admins-fvera@gcpsandbox.cloud --role=roles/resourcemanager.organizationAdmin
gcloud organizations add-iam-policy-binding 63734882150 \
--member=group:gcp-organization-admins-fvera@gcpsandbox.cloud --role=roles/resourcemanager.projectCreator
gcloud organizations add-iam-policy-binding 63734882150 \
--member=group:gcp-organization-admins-fvera@gcpsandbox.cloud --role=roles/securitycenter.admin
gcloud organizations add-iam-policy-binding 63734882150 \
--member=group:gcp-organization-admins-fvera@gcpsandbox.cloud --role=roles/serviceusage.serviceUsageConsumer
—————————————————————————————————————————
gcloud organizations add-iam-policy-binding 63734882150 \
--member=group:gcp-billing-admins-fvera@gcpsandbox.cloud --role=roles/billing.admin
gcloud organizations add-iam-policy-binding 63734882150 \
--member=group:gcp-billing-admins-fvera@gcpsandbox.cloud --role=roles/billing.creator
gcloud organizations add-iam-policy-binding 63734882150 \
--member=group:gcp-billing-admins-fvera@gcpsandbox.cloud --role=roles/billing.user
gcloud organizations add-iam-policy-binding 63734882150 \
--member=group:gcp-billing-admins-fvera@gcpsandbox.cloud --role=roles/billing.viewer
gcloud organizations add-iam-policy-binding 63734882150 \
--member=group:gcp-billing-admins-fvera@gcpsandbox.cloud --role=roles/resourcemanager.organizationViewer
—————————————————————————————————————————-
gcloud organizations add-iam-policy-binding 63734882150 \
--member=group:gcp-security-admins-fvera@gcpsandbox.cloud --role=roles/compute.viewer
gcloud organizations add-iam-policy-binding 63734882150 \
--member=group:gcp-security-admins-fvera@gcpsandbox.cloud --role=roles/container.viewer
gcloud organizations add-iam-policy-binding 63734882150 \
--member=group:gcp-security-admins-fvera@gcpsandbox.cloud --role=roles/iam.organizationRoleViewer
gcloud organizations add-iam-policy-binding 63734882150 \
--member=group:gcp-security-admins-fvera@gcpsandbox.cloud --role=roles/iam.securityReviewer
gcloud organizations add-iam-policy-binding 63734882150 \
--member=group:gcp-security-admins-fvera@gcpsandbox.cloud --role=roles/logging.configWriter
gcloud organizations add-iam-policy-binding 63734882150 \
--member=group:gcp-security-admins-fvera@gcpsandbox.cloud --role=roles/logging.privateLogViewer
gcloud organizations add-iam-policy-binding 63734882150 \
--member=group:gcp-security-admins-fvera@gcpsandbox.cloud --role=roles/orgpolicy.policyAdmin
gcloud organizations add-iam-policy-binding 63734882150 \
--member=group:gcp-security-admins-fvera@gcpsandbox.cloud --role=roles/orgpolicy.policyViewer
gcloud organizations add-iam-policy-binding 63734882150 \
--member=group:gcp-security-admins-fvera@gcpsandbox.cloud --role=roles/resourcemanager.folderIamAdmin
gcloud organizations add-iam-policy-binding 63734882150 \
--member=group:gcp-security-admins-fvera@gcpsandbox.cloud --role=roles/securitycenter.admin
—————————————————————————————————————————
gcloud organizations add-iam-policy-binding 63734882150 \
--member=group:gcp-network-admins-fvera@gcpsandbox.cloud --role=roles/compute.networkAdmin
gcloud organizations add-iam-policy-binding 63734882150 \
--member=group:gcp-network-admins-fvera@gcpsandbox.cloud --role=roles/compute.securityAdmin
gcloud organizations add-iam-policy-binding 63734882150 \
--member=group:gcp-network-admins-fvera@gcpsandbox.cloud --role=roles/compute.xpnAdmin
gcloud organizations add-iam-policy-binding 63734882150 \
--member=group:gcp-network-admins-fvera@gcpsandbox.cloud --role=roles/resourcemanager.folderViewer
gcloud organizations add-iam-policy-binding 63734882150 \
--member=group:gcp-network-admins-fvera@gcpsandbox.cloud --role=roles/compute.networkAdmin

————————————————————————————————————————————

- [x]  Asegurese de haber configurado correctamente su Billing Account a su proyecto Pivote Inicial
- [x]  Crear Cloud Identity o Google Workspace ( G-suite) groups par su organizacion y administracion de facturacion ( Usar G-suite si su proyecto pertenece a una Organizacion no Creada ya que debera tener la capacidad de recibir correos de notificacion de aumento de Quota de Proyectos a 50.
- [x]  Agregar usuario que usaran Terraform a el grupo group_org_admins. Ellos tienen que pertencer dentro de eso grupo, o ellos no tendran el rol de roles/resourcemanger.projectCreator
- [x]  Para los usuarios que correran procedimientos en este documento, garantizar los siguientes roles :
- El rol de roles/billing.admin sobre el Billing Account
- El rol de  roles/resourcemanger.folderCreator role
- [x]  Clonar el repositorio git original del terraform-foundation-example en su ultima version 2.3.0 dentro de una carpeta de su preferencia  con el comando

      git clone https://github.com/terraform-google-modules/terraform-example-foundation.git

# Que es Terraform-example-foundation ?

Este es un repositorio de muestra que muestra cómo se pueden componer los módulos CFT Terraform para construir una base de GCP segura, siguiendo la guía de bases de seguridad de Google Cloud. La estructura y el código proporcionados están destinados a formar un punto de partida para construir su propia base con valores pragmáticos predeterminados que puede personalizar para satisfacer sus propios requisitos. Actualmente, el paso 0 se ejecuta manualmente. Desde el paso 1 en adelante, el código de Terraform se implementa aprovechando Google Cloud Build (de forma predeterminada) o Jenkins. Cloud Build se eligió de forma predeterminada para permitir a los equipos comenzar rápidamente sin la necesidad de implementar una herramienta de CI / CD, aunque vale la pena señalar que el código se puede ejecutar fácilmente con su herramienta preferida.

# Introducion

Esta bitacora pretende dar  a los Arquitectos Cloud, Devops Cloud y Sysadmin Cloud y desarolladores en general una guia paso a paso y detallada de la ejecucion de codigo fuente para el despliegue del terraform-foundation example encontrado en la siguiente ruta :

![https://cdn.icon-icons.com/icons2/2368/PNG/512/github_logo_icon_143772.png](https://cdn.icon-icons.com/icons2/2368/PNG/512/github_logo_icon_143772.png)

   **Url**: [https://github.com/terraform-google-modules/terraform-example-foundation/tree/v2.3.0](https://github.com/terraform-google-modules/terraform-example-foundation/tree/v2.3.0)

# Agradecimiento y contribuyentes:

Agradecimientos por tan excelente trabajo de desarollo 👉🏼  [+45 Contribuyentes](https://github.com/terraform-google-modules/terraform-example-foundation/graphs/contributors) de tan excelente codigo de IaaC - CI/CD del terraform expample foundation sobre GCP,  y el equipo de Cloud Ops del proyecto Itaka - Kerlaty ( Fabian Vera, Gustavo Zocco y Arturo Guaracha )

# 🛡️ **EJECUCION**

# 0-bootstrap Deploying with Cloud Build

1. Ingrese al Folder **0-bootstrap** folder.
2. Renombre el archivo terraform.example.tfvars to terraform.tfvars y actualize el archivo con los valores de su ambiente. usando el siguiente comando :
**mv terraform.example.tfvars terraform.tfvars**

 terraform.tfvars ---(Este es un ejemplo didactico de lo que necesitara cambiar en los valores )-

org_id = "63734882150" 

Billing acount: 0190EC-8A1C41-B39182 

group_org_admins = "[gcp-organization-admins@noaharrozymar.com.co](mailto:gcp-organization-admins@noaharrozymar.com.co)"

group_billing_admins = "[gcp-billing-admins@noaharrozymar.com.co](mailto:gcp-billing-admins@noaharrozymar.com.co)"

audit_data_users = "[gcp-security-admins@noaharrozymar.com.co](mailto:gcp-security-admins@noaharrozymar.com.co)"

default_region = "us-central1"

Importante:

Si se va a desplegar de una organizacion que ya posee folders deben indicarle el ID de Parent folder.

Parent Folder = 511111564246 

3: Antes de ejecutarlo  tcomando $t**erraform plan** ejecutar :  $gcloud auth application-default login
y luego si ejecutar el   comando **terraform plan**

3.1 Para correr el  terraform-validator porfavor siga los paso de como Instalar Terraform Validator en instale la version 0.4.0 Usted tambien necesitara el binario de **terraform-validator-<your-platform> to terraform-validator** y el  terraform-validator binary tiene que estar en su  PATH.

4. Ejecute el comando **terraform plan -input=false -out bootstrap.tfplan**

5.Ejecute el comando **terraform show -json bootstrap.tfplan > bootstrap.json**

 🚧  **IMPORTANTE!**
6.Antes de eso verificar que la Cloud Resource Manager API este habilitado en el proyecto pivote  <project-id del proyecto pivote>

7.Ejecute el comando t**erraform-validator validate bootstrap.json --policy-path="../policy-library" --project <project-id del proyecto pivote>** y valide las violaciones de  **<project-id del proyecto pivote>** que puedan existir en el proyecto, esto es necesario porque Terraform-validator  enlazar los recurso valid Google Cloud Platform project).

Nota el output que generara es de : No violation found

8.Ejecute el comando  **terraform apply**.

📒 **NOTA:** Esperar 10 minutos minimo a que termine el terraform apply y muestre la totalidad de recursos.

7.Ejecutar el comando **terraform output terraform_service_account
terraform output terraform_service_account**

Output:

👉🏼 [org-terraform@prj-b-seed-b716.iam.gserviceaccount.com](mailto:org-terraform@prj-b-seed-b716.iam.gserviceaccount.com) 

Con esto obtendra una direccion de correo electronico de el admin, la cual necesitara en posteriores procedimiento por favor guardela. 

9.Ejecute el comando **terraform output gcs_bucket_tfstate**

Output: Obtendra un valor como este del ejemplo

**bkt-b-tfstate-fc1b** 

10.Copie el archivo [backend.tf](http://backend.tf).example a  [backend.tf](http://backend.tf/) ejecutnado el comando
**cp backend.tf.example [backend.tf](http://backend.tf/)**

11: Actualice los valores del archivo  [backend.tf](http://backend.tf/) con el nombre de su  Cloud Storage bucket, obtenido en el paso 8.

12: Vuelva a correr el comando  **terraform init**. When you're prompted, agree to copy state to Cloud Storage.
👀 (Optional) Correr el comando  t**erraform apply** tpara verificar que el estado esta configurado correctamente. Usted debera ver que no hay cambio en el anterior estado state.

[Inputs](https://www.notion.so/309a059549004aa8aa14390cb8ce5de1)

[Outputs](https://www.notion.so/fb38ec31f43a4226bb4884cbe9091135)

# 1-org

Este repositorio es parte de una guía de varias partes que muestra cómo configurar e implementar la arquitectura de referencia de [example.com](http://example.com/) descrita en la guía de bases de seguridad de **Google Cloud (PDF)**. La siguiente tabla enumera las partes de la guía.

## **Datos Requerimientos**

- Organization ID = "63734882150"
- Projecto ID = prj-b-cicd-abf1
- Project number = 726067341288
- Service account : [org-terraform@prj-b-seed-b716.iam.gserviceaccount.com](mailto:org-terraform@prj-b-seed-b716.iam.gserviceaccount.com)

# 🚧 Para evitar error por roles en CI/CD en la Service Account

1. Ejecutar  el siguiente comando : **gcloud organizations add-iam-policy-binding 63734882150 
[-member=serviceAccount:726067341288@cloudbuild.gserviceaccount.com](mailto:--member=serviceAccount:726067341288@cloudbuild.gserviceaccount.com) --role=roles/iam.securityReviewer** 

2. Darle permisos de Security Reviewer a nivel de Organizacion a la Service Account de Bootstrap ( [prj-b-seed-b716.iam.gserviceaccount.com](http://prj-b-seed-b716.iam.gserviceaccount.com/)) .

2.1 Ejecutar gcloud scc notifications describe scc-notify --organization=63734882150 [-impersonate-service-account=org-terraform@prj-b-seed-b716.iam.gserviceaccount.com](mailto:--impersonate-service-account=org-terraform@prj-b-seed-b716.iam.gserviceaccount.com) -SANBOX ( 11-4-201)

**EJECUCION:**
1. Ejecutar **gcloud source repos clone gcp-policies --project=prj-b-cicd-abf1** 

2: Navigate dentro de repositorio **gcp-policies** repo.
Ejecute el comando : **cd gcp-policies**

3: Ejecutar gcloud source repos clone gcp-org --project=prj-b-cicd-abf1

🚧  **IMPORTANTE!**
\gcp-policies\policies\templates\gcp_network_enable_flow_logs_v1.yaml
enable_flow_logs == true from false

4:Navigate into the repo and change to a non-production branch. All subsequent steps assume you are running them from the gcp-environments directory. If you run them from another directory, adjust your copy paths accordingly.
cd gcp-org

5: 🛡️EJECUCION

Ejecutar **git checkout -b plan**

6:🛡️EJECUCION

Copiar el contenido del nuevo foundation (las variables de terraform se actualizarán en un paso futuro).

7:🛡️EJECUCION

Ejecutar comando: **cp -RT ../terraform-example-foundation/1-org/ .**

8:🛡️EJECUCION

Copie los archivos de configuración de Cloud Build para Terraform. Es posible que deba modificar el comando para reflejar su directorio actual.
9:🛡️EJECUCION

Ejecutar el comando **cp ../terraform-example-foundation/build/cloudbuild-tf-* .**

10:.🛡️EJECUCION

Copie el script de envoltura de Terraform en la raíz de su nuevo repositorio (modifíquelo en consecuencia según su directorio actual).

Ejecutar el comando: **cp ../terraform-example-foundation/build/tf-wrapper.sh .**

11🛡️EJECUCION

Asegúrese de que se pueda ejecutar el script contenedor.
Ejecutar el comando: **sudo  chmod 755 ./tf-wrapper.sh**

12.🛡️EJECUCIONCompruebe si su organización ya tiene una política de administrador de contexto de acceso.
**Prerrequisitos:**

- Organizacion ID "63734882150"
- gcloud access-context-manager policies list --organization 63734882150 --format="value(name)"

Outputs:
**546568292840**

13.✅ **Prerequisitos**
Antes de ejecutar el paso 14 Verificar  permisos de Security Reviewer a la cuenta  [PROJECT_NUM@cloudbuild.gserviceaccount.com](mailto:PROJECT_NUM@cloudbuild.gserviceaccount.com) , asi como la sa [org-terraform@prj-b-seed-3bdb.iam.gserviceaccount.com](mailto:org-terraform@prj-b-seed-3bdb.iam.gserviceaccount.com)
sino los tiene asignarlos.

🛡️EJECUCION
Renombre y actualice el archivo con valores de **./envs/shared/terraform.example.tfvars to ./envs/shared/terraform.tfvars** su entorno y el paso de arranque (puede volver a ejecutar la salida de terraform en el directorio 0-bootstrap para encontrar estos valores). Asegúrate de que default_region esté configurado en una región de conjunto de datos de BigQuery válida. Además, si el paso anterior mostró un valor numérico, asegúrese de quitar los comentarios de la variable create_access_context_manager_access_policy = false. Consulte la carpeta compartida README.md para obtener información adicional sobre los valores del archivo terraform.tfvars.

🚧 **IMPORTANTE** que el archivo ./envs/shared/terraform.tfvars  quede con los valores incluidos

- create_access_context_manager_access_policy = false
- enable_hub_and_spoke = true

**14** ✅ **Prerequisitos**
Comentar del archivo gcp-org/envs/shared/scc_notification el TODO EL RECURSO resource "google_scc_notification_config" "scc_notification_config"

15 .Asegurate de actualizar backend en el archivo [backend.tf](http://backend.tf/)
bkt-b-tfstate-fc1b ( Ejemplo de valor obtenido)

🛡️ **EJECUCION**
**Commit de Cambios**

- Ejecutar el comando : **git add .**
- Ejecutar el comando : **git commit -m "Carga gcp-org 11-4-2021"**

16: ✅**Prerrequisitos:**
Ejecutar antes el comando **gcloud auth application-default login ( Como medida preventiva)**

Push la rama de su plan para activar un plan. Para este comando, el plan de la rama no es especial. Cualquier rama cuyo nombre sea diferente al de desarrollo, no producción o producción activará un plan de Terraform.
Ejecuta el comando: **git push --set-upstream origin plan**

🛡️ 🔄 **DURANTE LA EJECUCION**

- Ejecutar el comando **git add --chmod=+x [tf-wrapper.sh](http://tf-wrapper.sh/)**   ( Como medida preventiva )
- Ejecutar el comando gcloud auth application-default login ( Como medida preventiva )

 🛡️ **EJECUCION**

- gcloud scc notifications describe scc-notify--organization=63734882150

🚧 **IMPORTANTE** 
VERFICAR QUE ESTE COMENTADO  el recurso del archivo  scc_notification_config.tf file
resource "google_scc_notification_config" "scc_notification_config" una vez verificando, proceder a pasar a produccion.

🛡️ **EJECUCION**
Merge changes to production branch.

Ejecutar el comando **git checkout -b production**
Ejecutar el comando **git push origin production**

# 2-enviroments

1.✅**Prerrequisitos:**
Tener a la mano el project Id = prj-b-cicd-abf1 

1.1 🛡️ **EJECUCION** 

Ejecutar el comando cd .. 

2.🛡️ **EJECUCION** 

Ejecutar comando **gcloud source repos clone gcp-environments --project=prj-b-cicd-abf1** 

3.🛡️ **EJECUCION**

Navegue al repositorio y cambie a la rama no maestra. Todos los pasos posteriores asumen que los está ejecutando desde el directorio gcp-environment. Si los ejecuta desde otro directorio, ajuste sus rutas de copia en consecuencia.

- Ejecutar el comando: **cd gcp-environments**
- Ejecutar el comando: **git checkout -b plan**

4.🛡️ **EJECUCION**

Copie el contenido de la base en un nuevo repositorio.

- Ejecutar el comando **cp -RT ../terraform-example-foundation/2-environments/ .**
- Copie los archivos de configuración de compilación en la nube para Terraform, ejcutar
**cp ../terraform-example-foundation/build/cloudbuild-tf-* .**

      Copie el script de contenedor de Terraform en la raíz de su nuevo repositorio.

- Ejecutar el comando **cp ../terraform-example-foundation/build/tf-wrapper.sh .**

5.🛡️ **EJECUCION**

Asegurese que **wrapper scrip**t puede ser ejecutado.
Ejecutar el comando: **sudo chmod 755 ./tf-wrapper.sh**

6:✅**Prerrequisitos**

Tener a la mano la siguiente informacion :
Service account : [org-terraform@prj-b-seed-b716.iam.gserviceaccount.com](mailto:org-terraform@prj-b-seed-b716.iam.gserviceaccount.com) 
Bucket Name : bkt-b-tfstate-fc1b 

🛡️ **EJECUCION**
Renombrar el archivo **terraform.example.tfvars** a **terraform.tfvars** 

**y actualice el archivo con los valores de su entorno y bootstrap (puede volver a ejecutar la salida de terraform en el directorio 0-bootstrap para encontrar estos valores).** 

Consulte cualquiera de los archivos README.md de la carpeta envs para obtener información adicional sobre los valores del archivo terraform.tfvars.

🚧 **IMPORTANTE** 
Actualice los bakends de todos los ambientes

7.✅**Prerrequisitos**

Tener a la mano la siguiente informacion :
Service account : [org-terraform@prj-b-seed-b716.iam.gserviceaccount.com](mailto:org-terraform@prj-b-seed-b716.iam.gserviceaccount.com) 
Bucket Name : bkt-b-tfstate-fc1b 

Tener a la mano la siguiente informacion :
Service account : [org-terraform@prj-b-seed-b716.iam.gserviceaccount.com](mailto:org-terraform@prj-b-seed-b716.iam.gserviceaccount.com) 
Bucket Name : bkt-b-tfstate-fc1b 
🛡️ **EJECUCION**
Commit cambios.

- Ejecutar comando : **git add .**
- **git commit -m** 'Primera carga gcp-environments'

8.🛡️ **EJECUCION**
Push de la rama de su plan para activar un plan para todos los entornos.

- **git push --set-upstream origin plan**

🛡️ 🔄 **DURANTE LA EJECUCION**

Tambien ejecutar despues de hacer el push en cada ambiente (plan-develovment-nonproduction - Production)
Ejecutar el comando **git add --chmod=+x [tf-wrapper.sh](http://tf-wrapper.sh/)**  ( Como medida preventiva en caso  de que no tome los cambios en el sudo chmod +x tf-wrapper.sh

9:🛡️ **EJECUCION**
Revise el resultado del plan en su proyecto de compilación en la nube [https://console.cloud.google.com/cloud-build/builds?project=YOUR_CLOUD_BUILD_PROJECT_ID](https://console.cloud.google.com/cloud-build/builds?project=YOUR_CLOUD_BUILD_PROJECT_ID)

10.✅**Prerrequisitos**

🚧 **IMPORTANTE**  buscar el bucket de cada ambiente despues de que push a la branch plan haya sido aplicado correctamente  y borrar el archivo default.tfstate (a medida que se va haciendo push en cada ambiente)

10.1🛡️ **EJECUCION**
Review the apply output in your cloud build project [https://console.cloud.google.com/cloud-build/builds?project=YOUR_CLOUD_BUILD_PROJECT_ID](https://console.cloud.google.com/cloud-build/builds?project=YOUR_CLOUD_BUILD_PROJECT_ID)

11.✅**Prerrequisitos**
🚧 **IMPORTANTE** buscar el bucket de cada ambiente despues de que push a la branch plan haya sido aplicado correctamente  y borrar el archivo **default.tfstate** (a medida que se va haciendo push en cada ambiente)

🛡️ **EJECUCION**
git add --chmod=+x [tf-wrapper.sh](http://tf-wrapper.sh/)                   ...importante!!!

- Ejecutar el comando : **git checkout -b non-production**
- Ejecutar el comando : **git push origin non-production**
- Ejecutar el comando **git add --chmod=+x [tf-wrapper.sh](http://tf-wrapper.sh/)**  ( Como medida preventiva en caso  de que no tome los cambios en el sudo chmod +x tf-wrapper.sh

12.🛡️ **EJECUCION**

Revise el resultado de la aplicación en su proyecto de compilación en la nubet [https://console.cloud.google.com/cloud-build/builds?project=YOUR_CLOUD_BUILD_PROJECT_ID](https://console.cloud.google.com/cloud-build/builds?project=YOUR_CLOUD_BUILD_PROJECT_ID)

13.✅ **Prerequisitos**

🚧 **IMPORTANTE**  buscar el bucket de cada ambiente despues de que push a la branch plan haya sido aplicado correctamente  y borrar el archivo default.tfstate (a medida que se va haciendo push en cada ambiente)

🛡️ **EJECUCION**
Merge cambios a la rama produccion.

- Ejecutar el comando **git checkout -b production**
- Ejecutar el comando  **git push origin production**
- Ejecutar el comando  g**it add --chmod=+x [tf-wrapper.sh](http://tf-wrapper.sh/)**

14.🛡️ **EJECUCION**
Revise el resultado de la aplicación en su proyecto de compilación en la nube [https://console.cloud.google.com/cloud-build/builds?project=YOUR_CLOUD_BUILD_PROJECT_ID](https://console.cloud.google.com/cloud-build/builds?project=YOUR_CLOUD_BUILD_PROJECT_ID)

15.🛡️ **EJECUCION**
Ahora puede pasar a las instrucciones del paso 3: redes

# 3-Networking

✅ **Prerequisitos Generales**

Tener a la mano  los siguiente datos
Org ID = "63734882150" 

Backet Name = bkt-b-tfstate-fc1b

- Ejecutado satisfactoriamente 0-bootstrap
- Ejecutado satisfactoriamente 1-org
- Ejecutado satisfactoriamente 2-environments
- Obtenga el valor de la variable access_context_manager_policy_id. Puede obtenerse ejecutando **gcloud access-context-manager policies list --organization YOUR_ORGANIZATION_ID --format="value(name)"**

output:
gcloud access-context-manager policies list --organization 63734882150 --format="value(name)" --
546568292840  

1.🛡️ **EJECUCION**

Ejecutar el comando **cd ..**

2.✅ **Prerequisitos** 
Tener a la mano los siguiente datos :
Project Id CI/CD = prj-b-cicd-abf1 

🛡️ **EJECUCION**
Ejecutar el siguiente comando gcloud s**ource repos clone gcp-networks --project=prj-b-cicd-abf1**

3.🛡️ **EJECUCION**
Change to the freshly cloned repo and change to non-master branch.
git checkout -b plan

- Cambiar a reciente repo gcp-networks
Ejecutar el siguiente comando  **cd gcp-networks**
- Cambie al repositorio recién clonado y cambie a la rama no maestra.
Ejecutar el siguiente comando **git checkout -b plan**

🚧 **IMPORTANTE**  

- Renombrar el archivo  **vpn.tf.example** to **[vpn.tf](http://vpn.tf/)** in each environment folder in 3-networks/envs/<ENV>. ( NO HACERLO SI AUN NO CONFIGURARA LA VPN)
- Cambiar links simbolicos SI Y SOLO SI ESTEN ROTOS comando : ln -s ../shared/access_context.auto.tfvars access_context.auto.tfvars en todos los ambientes.

4.🛡️ **EJECUCION**
Copie el contenido del foundationen un nuevo repositorio.

- Ejecute el comando **cp -RT ../terraform-example-foundation/3-networks/ .**

5.🛡️ **EJECUCION**
Copie los archivos de configuración de Cloud Build para Terraform.

- Ejecutar el siguiente comando

6.🛡️ **EJECUCION**
Copie el script de contenedor de Terraform en la raíz de su nuevo repositorio.

- Ejecutar el siguiente comando **cp ../terraform-example-foundation/build/tf-wrapper.sh .**

7.🛡️ **EJECUCION**
Asegúrese de que se pueda ejecutar el script contenedor.

- Ejecutar el siguiente comando **sudo chmod 755 ./tf-wrapper.sh**

8.✅ **Prerequisitos** 

Tener a la mano lo siguientes Datos:
org_id = "63734882150" 
Service account : [org-terraform@prj-b-seed-b716.iam.gserviceaccount.com](mailto:org-terraform@prj-b-seed-b716.iam.gserviceaccount.com)  
Paremt Folder : 511111564246  ( si y solo si , ya existe la organizacion y el nuevo despliegue procede de un folder predefinido previamente).

🛡️ **EJECUCION**
Cambie el nombre de common.auto.example.tfvars a common.auto.tfvars y actualice el archivo con los valores de su entorno y bootstrap.
Consulte cualquiera de los archivos [README.md](http://readme.md/) de la carpeta envs para obtener información adicional sobre los valores del archivo common.auto.tfvars.

IMPORTANTE DEJAR ESTOS VALORES HABILITADOS en el archivo common.auto.tfvars

enable_hub_and_spoke = true

//enable_hub_and_spoke_transitivity = false

I🚧 **IMPORTANTE**   Actualizar los archivos  backend en Cada uno de los ambientes gcp-networks/envs/development ,gcp-networks/envs/non-production ,gcp-networks/envs/production
AUN NO HACERLO Paso de la VPN: en el archivo [vpn.tf](http://vpn.tf/) (DEJARLO vpn.tf.example), actualice los valores para el entorno, vpn_psk_secret_name, on_prem_router_ip_address1, on_prem_router_ip_address2 y bgp_peer_asn

9.
Cambie el nombre de shared.auto.example.tfvars a shared.auto.tfvars y actualice el archivo con target_name_server_addresses (la lista de servidores de nombres de destino para la zona de reenvío de DNS en el concentrador de DNS).

10. 🛡️ **EJECUCION**
Cambie el nombre de access_context.auto.example.tfvars a access_context.auto.tfvars y actualice el archivo con el access_context_manager_policy_id.

11.🛡️ **EJECUCION**
Commit cambios

- Ejecutar el siguiente comando **git add .**
- Ejecutar el siguiente comando git commit -m 'Primera Carga gcp-networks fecha'

12.🛡️ **EJECUCION**
Debe planificar y aplicar manualmente el entorno compartido (solo una vez) ya que los entornos de desarrollo, no producción y producción dependen de él.

- Ejecutar el siguiente comando **cd ./envs/shared/.**
- Verificar Actualice [backend.tf](http://backend.tf/) con el nombre de su depósito desde el paso 0-bootstrap.
- Ejecutar el siguiente comando  **terraform init**
- Ejecutar el siguiente comando **terraform plan** y revise la salida.
- Ejecutar el siguiente comando  **terraform aply.** y verificar la salida de revisión:

Output: Aplicar completo! Recursos: 69 agregados, 0 modificados, 0 destruidos

- Push a la rama de su plan para disparar un plan.

Ejecutar el siguiente comando **git push --set-upstream origin plan** 

(wait to finish)

--------------------------------examplefile.tfvars-----------------------------------------

org_id = "63734882150"

terraform_service_account = "[org-terraform@prj-b-seed-94ab.iam.gserviceaccount.com](mailto:org-terraform@prj-b-seed-94ab.iam.gserviceaccount.com)"

default_region1 = "us-central1"

default_region2 = "us-west1"

// The DNS name of peering managed zone. Must end with a period.
domain = "[noaharrozymar.com.co](http://noaharrozymar.com.co/)."

// Optional - for an organization with existing projects or for development/validation.
// Must be the same value used in previous steps.
parent_folder = "253572731245"

enable_hub_and_spoke = true

//enable_hub_and_spoke_transitivity = false

---------------------------------- *********************** ----------------------------------------------

13.🛡️ **EJECUCION**
Debe ejecutar manualmente el   plan y aply  en el entorno compartido (solo una vez) ya que los entornos de desarrollo, no producción y producción dependen de él.

- Ejecutar el siguiente comando  **cd ./envs/shared/**
- Acutalice backend.tf con el nombre de su depósito del paso 0-bootstrap.
- Ejecutar el siguiente comando  **terraform init.**
- Ejecutar el siguiente comando **terraform plan** y revisar el resultado
- Ejecutar el siguiente comando **terraform apply.**
- Si desea que el depósito sea reemplazado por Cloud Build en el tiempo de ejecución, vuelva a cambiar el nombre del bucket a UPDATE_ME.

14.✅ **Prerequisitos** 
VERFICAR  \gcp-policies\policies\templates\gcp_network_enable_flow_logs_v1.yaml
enable_flow_logs == true

🛡️ **EJECUCION**

Push de la rama de su plan para activar un plan para todos los entornos. Debido a que la rama del plan no es una rama de entorno con nombre, presionar la rama del plan activa terraform plan pero no se aplica terraform.

- Ejecutar el siguiente comando  **git push --set-upstream origin plan**

15.🛡️ **EJECUCION**
Revisa el resultado del plan en tu proyecto de Cloud Build [https://console.cloud.google.com/cloud-build/builds?project=YOUR_CLOUD_BUILD_PROJECT_ID](https://console.cloud.google.com/cloud-build/builds?project=YOUR_CLOUD_BUILD_PROJECT_ID)

16.🛡️ **EJECUCION**
Una vez aplicada la producción, aplique el revelado.

17.🛡️ **EJECUCION**
Merge cambios a development.

- Ejecutar el siguiente comando **git checkout -b development**
- Ejecutar el siguiente comando **git push origin development**

18.🛡️ **EJECUCION**
Revisa el resultado del plan en tu proyecto de Cloud Build [https://console.cloud.google.com/cloud-build/builds?project=YOUR_CLOUD_BUILD_PROJECT_ID](https://console.cloud.google.com/cloud-build/builds?project=YOUR_CLOUD_BUILD_PROJECT_ID)

19.🛡️ **EJECUCION**
Después de que se haya aplicado el desarrollo, aplique no producción.

20.🛡️ **EJECUCION**
Merge cambios a non-production.

- Ejecutar el siguiente comando  **git checkout -b non-production**
- Ejecutar el siguiente comando  **git push origin non-production**

21.🛡️ **EJECUCION**
Revisa el resultado del plan en tu proyecto de Cloud Build [https://console.cloud.google.com/cloud-build/builds?project=YOUR_CLOUD_BUILD_PROJECT_ID](https://console.cloud.google.com/cloud-build/builds?project=YOUR_CLOUD_BUILD_PROJECT_ID)

22.🛡️ **EJECUCION**
Ahora puede pasar a las instrucciones del paso 4-proyectos.

////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

# TROUBLESHOOTING PARA HACER ANDAR LOS ROUTERS

Adiicionar  estos Output en el  archivo [output.tf](http://output.tf/) de (gcp-networks/envs/non-production) - PADRE
#######

# Outputs for debuging routers not created

output "Test_out_child_module_out" {
value = module.base_shared_vpc.Test_child_value_out
}

output "base_shared_vpc_count" {
value       = module.base_shared_vpc.base_shared_vpc_count
}

output "base_shared_vpc_vpc_name" {
value       = module.base_shared_vpc.base_shared_vpc_vpc_name
}

output "base_shared_vpc_def_region1" {
value       = module.base_shared_vpc.base_shared_vpc_def_region1
}

output "base_shared_vpc_project_id" {
value       = module.base_shared_vpc.base_shared_vpc_project_id
}

output "base_shared_vpc_net_name" {
value       = module.base_shared_vpc.base_shared_vpc_net_name
}
output "base_shared_vpc_bgp_asn" {
value       = module.base_shared_vpc.base_shared_vpc_bgp_asn_subnet
}

Step #4 - "tf apply": Test_out_child_module_out = n-shared-base-spoke
Step #4 - "tf apply": base_host_project_id = prj-n-shared-base-4d94
Step #4 - "tf apply": base_network_name = vpc-n-shared-base-spoke
Step #4 - "tf apply": base_network_self_link = [https://www.googleapis.com/compute/v1/projects/prj-n-shared-base-4d94/global/networks/vpc-n-shared-base-spoke](https://www.googleapis.com/compute/v1/projects/prj-n-shared-base-4d94/global/networks/vpc-n-shared-base-spoke)
Step #4 - "tf apply": base_project_id_anidado = prj-n-shared-base-4d94
Step #4 - "tf apply": base_shared_vpc_bgp_asn = 64514
Step #4 - "tf

main .tf  (gcp-networks/envs/non-production)
1 Ejecutar esto comando gcloud
parend_id  ='MI parend Folder'
gcloud projects list --filter "parent.id='1007820506444' AND labels.application_name:base-shared-vpc-host AND  labels.environment:non-production AND lifecycleState:ACTIVE"

filter = "[parent.id](http://parent.id/):${split("/", data.google_active_folder.env.name)[1]} labels.application_name=base-shared-vpc-host labels.environment=${local.env} lifecycleState=ACTIVE"

2..Luego verificar si el  INDEX de esta expresion corresponde 0  y/o  1

(gcp-networks/modules/base_shared_vpc ) archivo [output.tf](http://output.tf/)  (HIJO)

#####################################################################################################

# Outputs for debuging routers not created

output "base_shared_vpc_count" {
value       = var.mode != "spoke" ? 1 : 0
}

output "base_shared_vpc_vpc_name" {
value       = local.vpc_name
}

output "base_shared_vpc_def_region1" {
value       = var.default_region1
}

output "base_shared_vpc_project_id" {
value       = var.project_id
}

output "base_shared_vpc_net_name" {
value       = module.main.network_name
}

output "base_shared_vpc_bgp_asn_subnet" {
value       = var.bgp_asn_subnet

Nota:
EL ROUTER SE CREARIA EN EL FOLDER  DE GUSTAVO fldr-non-production  CON PROJECID 1007820506444 en proyecto prj-n-shared-base	prj-n-shared-base-4d94

//////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

Prerequisites

org_id = "63734882150"
0-bootstrap executed successfully.

1-org executed successfully.

2-environments executed successfully.

3-networks executed successfully.

5- Obtain the value for the access_context_manager_policy_id variable.

gcloud access-context-manager policies list --organization 546568292840 --format="value(name)"

Access_Manager_Policy_Id = 546568292840

6-For the manual step described in this document, you need Terraform version 0.13.7 to be installed.

Note: Make sure that you use the same version of Terraform throughout this series. Otherwise, you might experience Terraform state snapshot lock errors.

7-gcloud access-context-manager perimeters list --policy ACCESS_CONTEXT_MANAGER_POLICY_ID --format="value(name)"
gcloud access-context-manager perimeters list --policy 546568292840 --format="value(name)" -- SANDBOX ( 9-11-2021)
Note: If you have more than one service perimeter for each environment, you can also get the values from the restricted_service_perimeter_name output from each of the3-networks environments.

sp_c_shared_restricted_default_perimeter_9723
sp_c_shared_restricted_default_perimeter_3140
sp_p_shared_restricted_default_perimeter_83ea
spb_c_to_p_shared_restricted_bridge_83ea
sp_d_shared_restricted_default_perimeter_fc0a
spb_c_to_d_shared_restricted_bridge_fc0a
sp_n_shared_restricted_default_perimeter_cf0d
spb_c_to_n_shared_restricted_bridge_cf0d
sp_c_shared_restricted_default_perimeter_1134
sp_p_shared_restricted_default_perimeter_e982
spb_c_to_p_shared_restricted_bridge_e982
sp_d_shared_restricted_default_perimeter_0709
spb_c_to_d_shared_restricted_bridge_0709
sp_n_shared_restricted_default_perimeter_8972
spb_c_to_n_shared_restricted_bridge_8972
sp_c_shared_restricted_default_perimeter_32b3
sp_p_shared_restricted_default_perimeter_85e7
spb_c_to_p_shared_restricted_bridge_85e7
sp_d_shared_restricted_default_perimeter_6a01
spb_c_to_d_shared_restricted_bridge_6a01
sp_n_shared_restricted_default_perimeter_fbab
spb_c_to_n_shared_restricted_bridge_fbab

If you are using Cloud Build you can also search for the values in the outputs from the build logs:

----------------------- DEVELOPMENT -------------------------------------------------------------------------------

gcloud builds list \
--project=prj-b-cicd-abf1 \
--filter="status=SUCCESS \
AND source.repoSource.repoName=gcp-networks \
AND substitutions.BRANCH_NAME=development" \
--format="value(id)"

output : e6b1181f-3b96-40a2-a946-551c27a6c6db

Use the result of this command as the BUILD_ID value in the next command:

gcloud builds log BUILD_ID \
--project=YOUR_CLOUD_BUILD_PROJECT_ID | \
grep "restricted_service_perimeter_name = "

gcloud builds log e6b1181f-3b96-40a2-a946-551c27a6c6db \
--project=prj-b-cicd-abf1  | \
grep "restricted_service_perimeter_name = "

out = Step #4 - "tf apply": restricted_service_perimeter_name = sp_d_shared_restricted_default_perimeter_0709

------------- NON-PRODUCTION ----------------------------------------------------------------------------------

gcloud builds list \
--project=prj-b-cicd-abf1 \
--filter="status=SUCCESS \
AND source.repoSource.repoName=gcp-networks \
AND substitutions.BRANCH_NAME=non-production" \
--format="value(id)"

outputs : cc4d2b17-0311-4924-8a09-41bd9a4a0afc

Use the result of this command as the BUILD_ID value in the next command:

gcloud builds log BUILD_ID \
--project=YOUR_CLOUD_BUILD_PROJECT_ID | \
grep "restricted_service_perimeter_name = "

Use the result of this command as the BUILD_ID value in the next command:

gcloud builds log cc4d2b17-0311-4924-8a09-41bd9a4a0afc \
--project=prj-b-cicd-abf1 | \
grep "restricted_service_perimeter_name = "

outputs : Step #4 - "tf apply": restricted_service_perimeter_name = sp_n_shared_restricted_default_perimeter_8972

--------------------- PRODUCTION ----------------------------------------------------------------------------------

gcloud builds list \
--project=prj-b-cicd-abf1 \
--filter="status=SUCCESS \
AND source.repoSource.repoName=gcp-networks \
AND substitutions.BRANCH_NAME=production" \
--format="value(id)"

outputs: 9337f44b-27ef-41b3-a4de-aebc9402026b

gcloud builds log 9337f44b-27ef-41b3-a4de-aebc9402026b \
--project=prj-b-cicd-abf1 | \
grep "restricted_service_perimeter_name = "

outputs : Step #4 - "tf apply": restricted_service_perimeter_name = sp_p_shared_restricted_default_perimeter_e982

/////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

# **4-projects**Deploying with Cloud Build

1.🛡️ **EJECUCION**

Clonar repositorio

- Ejecutar el comando **gcloud source repos clone gcp-projects --project=prj-b-cicd-abf1**

2.🛡️ **EJECUCION**

Cambie el repositorio recién clonado y cambie a una rama non-master

- Ejecutar el comando **git checkout -b plan**

3.🛡️ **EJECUCION**

Copie el contenido del foundatgion en un nuevo repositorio.

- Ejecutar el comando cp -RT ../terraform-example-foundation/4-projects/ .

4.🛡️ **EJECUCION**

Copie los archivos de configuración de Cloud Build para Terraform.
Ejecutar el comando **cp ../terraform-example-foundation/build/cloudbuild-tf-* .**

5.🛡️ **EJECUCION**

Copie Terraform wrapper script en la raíz de su nuevo repositorio.

- Ejecutar el comando **cp ../terraform-example-foundation/build/tf-wrapper.sh .**

6.🛡️ **EJECUCION**

Asegurese que el  wrapper script puede ser ejecutado.

- Ejecutar el comando **sudo chmod 755 ./tf-wrapper.sh**

7.🛡️ **EJECUCION**

Cambie el nombre de common.auto.example.tfvars a common.auto.tfvars y actualice el archivo con los valores de su entorno y bootstrap. Consulte cualquiera de los archivos [README.md](http://readme.md/) de las carpetas envs de la unidad de negocio para obtener información adicional sobre los valores del archivo common.auto.tfvars.

8.🛡️ **EJECUCION**

Cambie el nombre de shared.auto.example.tfvars a shared.auto.tfvars y actualice el archivo con los valores de su entorno y bootstrap. Consulte cualquiera de los archivos [README.md](http://readme.md/) de las carpetas envs compartidas de la unidad de negocio para obtener información adicional sobre los valores en shared.auto.example.tfvars.

9.🛡️ **EJECUCION**

Cambie el nombre de development.auto.example.tfvars a development.auto.tfvars y actualice el archivo con el nombre_perímetro que comienza con sp_d_shared_restricted.

10.🛡️ **EJECUCION**

Cambie el nombre de non-production.auto.example.tfvars a non-production.auto.tfvars y actualice el archivo con el nombre_perímetro que comienza con sp_n_shared_restricted.

11.🛡️ **EJECUCION**

Cambie el nombre de production.auto.example.tfvars a production.auto.tfvars y actualice el archivo con el nombre_perímetro que comienza con sp_p_shared_restricted.

12.🛡️ **EJECUCION**

Cambie el nombre de access_context.auto.example.tfvars a access_context.auto.tfvars y actualice el archivo con el access_context_manager_policy_id.

13.🛡️ **EJECUCION**

Businenes Unit1

Debe planificar manualmente y aplicar solo una vez el entorno business_unit_1 / shared, ya que el desarrollo, la no producción y la producción dependen de él.
Ejecute cd ./business_unit_1/shared/.

14.🛡️ **EJECUCION**

Actualice [backend.tf](http://backend.tf/) con el nombre de su balde del 0-bootstrap step.
14.1 Ejecutar el comando  **terraform init.**
14.2 Ejecutar el comando  t**erraform plan** y revice la salida
14.3 Ejecutar el comando **terraform apply.**
14.4 Ejecutar el comando t**erraform output cloudbuild_sa**  para obtener la cuenta de servicio de compilación en la nube desde el paso de solicitud.

Output:

[829789824485@cloudbuild.gserviceaccount.com](mailto:829789824485@cloudbuild.gserviceaccount.com)

14.5 ISi desea que el depósito sea reemplazado por la compilación en la nube en el tiempo de ejecución, cambie el nombre del depósito a UPDATE_ME.

Businenes Unit2
15.🛡️ **EJECUCION**

Businenes Unit2

Debe planificar manualmente y aplicar solo una vez el entorno business_unit_2/shared environment since development, non-production, and production depend on it.

- Ejecute el comando  **cd ./business_unit_2/shared/.**

Actualice [backend.tf](http://backend.tf/) con el nombre de su depósito desde el 0-bootstrap step.
15.1 Ejecutar el comando  **terraform init**.
13.2 Ejecutar el comando t**erraform plan** y revice la salida.
15.3 Ejecutar el comando t**erraform apply**.
15.4 Ejecutar el comando terraform output cloudbuild_sa para obtener la cuenta de servicio de compilación en la nube desde el paso de solicitud.

Output:

terraform output cloudbuild_sa
[323407638837@cloudbuild.gserviceaccount.com](mailto:323407638837@cloudbuild.gserviceaccount.com)

15.5 Si desea que el depósito sea reemplazado por la compilación en la nube en el tiempo de ejecución, cambie el nombre del depósito a UPDATE_ME.

# 5-app-infra

✅ **Prerequisitos** 
0-bootstrap ejecutado satisfactoriamente
1-org ejecutado satisfactoriamente
2-environments ejecutado satisfactoriamente
3-networks ejecutado satisfactoriamente
4-projects ejecutado satisfactoriamente

1.🛡️ **EJECUCION**

Obtenga el ID del proyecto Infra Pipeline del paso anterior. Ejecute lo siguiente en la carpeta gcp-projects / business_unit_1 / shared.
terraform output cloudbuild_project_id
Output : prj-bu1-c-infra-pipeline-f2d7

2.🛡️ **EJECUCION**

Clone el repositorio de políticas. (Este repositorio tiene el mismo nombre que el repositorio creado en el paso 1-org, pero es de un proyecto diferente, es posible que deba cambiar el nombre del anterior para evitar una colisión si lo está clonando en la misma carpeta).gcloud source repos 

clone gcp-policies --project=YOUR_INFRA_PIPELINE_PROJECT_ID

- Ejecute el comando  gcloud source repos clone gcp-policies --project=prj-bu1-c-infra-pipeline-f2d7

3.🛡️ **EJECUCION**

Navega al repositorio. Todos los pasos posteriores asumen que los está ejecutando desde el directorio gcp-environment. Si los ejecuta desde otro directorio, ajuste sus rutas de copia en consecuencia.

- Ejecute el Comando cd gcp-policies

4.🛡️ **EJECUCION**

Copy contents of policy-library to new repo.

- Ejecute el Comando cp -RT ../terraform-example-foundation/policy-library/ .

5.🛡️ **EJECUCION**

Commit cambios.

- Ejecute el comando **git add .**
- Ejecute el comando  **git commit -m 'Your message'**

6.Push su rama maestra al nuevo repositorio.

- Ejecute el comando git push --set-upstream origin master

7.🛡️ **EJECUCION**

Navega fuera del repositorio.

- Ejecute el comando cd ..

8.🛡️ **EJECUCION**

Clona el repositorio bu1-example-app.

- Ejecute el comando gcloud source repos clone bu1-example-app --project=prj-bu1-c-infra-pipeline-f2d7

9.🛡️ **EJECUCION**

Navega al repositorio. Todos los pasos posteriores asumen que los está ejecutando desde el directorio gcp-environment. Si los ejecuta desde otro directorio, ajuste sus rutas de copia en consecuencia.

- Ejecute el comando  **cd bu1-ejemplo-aplicación**

10.🛡️ **EJECUCION**

Cambie el repositorio recién clonado y cambie a una rama no maestra.

- Ejecute el comando **git checkout -b plan**

11.🛡️ **EJECUCION**

Copie el contenido de la base en un nuevo repositorio.

- Ejecute el comando  **cp -RT ../terraform-example-foundation/5-app-infra/ .**

12.🛡️ **EJECUCION**

Copie los archivos de configuración de Cloud Build para Terraform.

- Ejecute el comando cp ../terraform-example-foundation/build/cloudbuild-tf-* .

13.🛡️ **EJECUCION**

Copie el script contenedor de Terraform en la raíz de su nuevo repositorio.

- Ejecute el comando **cp ../terraform-example-foundation/build/tf-wrapper.sh .**

14.🛡️ **EJECUCION**

Asegurese wrapper script puede ser ejecutado.

- Ejecute el comando  sudo chmod 755 ./tf-wrapper.sh

15.🛡️ **EJECUCION**

Cambie el nombre de common.auto.example.tfvars a common.auto.tfvars y actualice el archivo con los valores de su entorno y 0-bootstrap. Consulte cualquiera de los archivos [README.md](http://readme.md/) de las carpetas envs de la unidad de negocio 1 para obtener información adicional sobre los valores del archivo common.auto.tfvars.

16.🛡️ **EJECUCION**

Cambie el nombre de bu1-development.auto.example.tfvars a bu1-development.auto.tfvars y actualice el archivo con los valores de su entorno. (fldr-development / prject-bu1-d-sample-base) y ubicas el usuario en el IAM del proyecto que se parezca a esto o se asemeje a este nombre project-service-account @ prj-bu1-d-sample-base -c52a.iam.gserviceaccount.com

17.🛡️ **EJECUCION**

Cambie el nombre de bu1-non-production.auto.example.tfvars a bu1-non-production.auto.tfvars y actualice el archivo con los valores de su entorno. fldr-non-production / prject-bu1-n-sample-base) y ubicas el usuario en el IAM del proyecto que se parezca a esto o se asemeje a este nombre project-service-account @ prj-bu1-n-sample- [base-f512.iam.gserviceaccount.com](http://base-f512.iam.gserviceaccount.com/)

18.🛡️ **EJECUCION**

Cambie el nombre de bu1-production.auto.example.tfvars a bu1-production.auto.tfvars y actualice el archivo con los valores de su entorno. fldr-production / prject-bu1-p-sample-base) y ubicas el usuario en el IAM del proyecto que se parezca a esto o se asemeje a este nombre project-service-account @ prj-bu1-p-sample-base- [f512.iam.gserviceaccount.com](http://f512.iam.gserviceaccount.com/)

19.🛡️ **EJECUCION**

Commit cambios.

- Ejecute el comando **git add .**
- Ejecute el comando  git commit -m ''Production Buss 1''

20.🛡️ **EJECUCION**

Push la rama de su plan para activar un plan para todos los entornos.
git push --set-upstream origin plan

21.🛡️ **EJECUCION**

Revisa el resultado del plan en tu proyecto de Cloud Build [https://console.cloud.google.com/cloud-build/builds?project=YOUR_INFRA_PIPELINE_PROJECT_ID](https://console.cloud.google.com/cloud-build/builds?project=YOUR_INFRA_PIPELINE_PROJECT_ID)

22.🛡️ **EJECUCION**

Merge cambios a  development.

- Ejecute los comandos **git checkout -b development**
- Ejecute los comandos git push origin development

23.🛡️ **EJECUCION**

Revisa el resultado del plan en tu proyecto de Cloud Build [https://console.cloud.google.com/cloud-build/builds?project=YOUR_INFRA_PIPELINE_PROJECT_ID](https://console.cloud.google.com/cloud-build/builds?project=YOUR_INFRA_PIPELINE_PROJECT_ID)

24.🛡️ **EJECUCION**

Merge cambios a  non-production.

- Ejecute el comando **git checkout -b non-production**
- Ejecute el comando git push origin non-production

25.🛡️ **EJECUCION**

Revisa el resultado del plan en tu proyecto de Cloud Build [https://console.cloud.google.com/cloud-build/builds?project=YOUR_INFRA_PIPELINE_PROJECT_ID](https://console.cloud.google.com/cloud-build/builds?project=YOUR_INFRA_PIPELINE_PROJECT_ID)

26.Merge cambios a production branch
git checkout -b production

- Ejecute los comandos **git checkout -b production**
- Ejecute los comandos **git push origin production**

27.🛡️ **EJECUCION**

Revisa el resultado del plan en tu proyecto de Cloud Build [https://console.cloud.google.com/cloud-build/builds?project=YOUR_INFRA_PIPELINE_PROJECT_ID](https://console.cloud.google.com/cloud-build/builds?project=YOUR_INFRA_PIPELINE_PROJECT_ID)

28 😀 Finalizo  todo
