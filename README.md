# robinbobin_gnix

ДЗ Nginx - балансировка и отказоустойчивость.

## На вашей выполняющей машине(с ОС Linux Ubunta) должны быть выполнены следующие действия:
* установить terraform и настроить его работу через провайдер yandexcloud
* установить ansible
* подготовить Yndex Cloud к работе и установить интерфейс командной строки YC  
* поолучите API Key Yandex Cloud или IAM tokken с настроенными правами и созданным сервисным аккаунтом
* создайте пару ключей ssh id_rsa и убедитесь что они лежат тут ~/.ssh/
* скачайте архив "https://github.com/adammck/terraform-inventory/releases/download/v0.10/terraform-inventory_v0.10_linux_amd64.zip"
* создайте папку terraform-inventory в каталоге opt и распакуйте в нее выполняющий файл из архива
* выполнить команду "git clone https://github.com/NexusPolarius/robinbobin_gnix.git"
* перейдите в подкаталоге проекта terraform 
* переименуйте файл terraform.tfvars.example в terraform.tfvars и отредактируйте его своими параметрами(image_id = "fd879gb88170to70d38a" указать такой)
* выполнить команду "terraform init"
* выполнить команду "terraform validate"
* выполнить команду "terraform plan"
* выполнить команду "terraform apply" и подтвердить выполнение командой "yes"
* после окончания создания виртуальных машин выполните команду "TF_STATE=. ansible-playbook --inventory-file=/opt/terraform-inventory ../ansible/main.yml"
* после завершения установки софта в консоль будет выведен публичный ip, который нужно использовать в браузерной строке "http://<публичный ip>"


```mermaid
flowchart TB
    A1[Client1] --> |public ip|B
    A2[Client2] --> |public ip|B 
    A3[Client3] --> |public ip|B
    B[Nginx-balancing]
    B --> C[backend1] --> E
    B --> D[backend2] --> E
    E[DB]