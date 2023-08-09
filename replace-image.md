# Troca de Imagem no Docker em runtime


1) Antes de trocar a imagem, é recomendado que você salve os dados do banco de dados caso deseje restaurá-los posteriormente ou em caso de falha.
- Para salvar o banco de dados, execute o comando abaixo:
docker exec <postgres_container_name> pg_dump -U <POSTGRES_USER> <database_name> > backup.sql
- O comando para restaurar o banco de dados caso precise depois da atualização da imagem é:
docker exec -i <postgres_container_name> psql -U <POSTGRES_USER> -d <database_name> < backup.sql
- Caso queira salvar as imagens de sua interface também é necessário fazer backup do minio(https://min.io/). Para isso basta copiar os arquivos da pasta do minio na máquina ou usar a própria interface do minio. 

2) Para troca de imagem, você deve ir no arquivo docker-compose.yml, e achar a sessão da imagem desejada, como por exemplo 'ui', e substituir o repositório pelo repositório de sua nova imagem. Veja o exemplo abaixo:

> ui:
>   image: reportportal/service-ui:5.7.4

3) Após atualização da imagem no arquivo docker-compose.yml, para que sua aplicação reflita as alterações feitas na imagem é necessário executar o seguinte comando abaixo:

> docker-compose up -d

4) Espere o serviço novamente subir e verique as mudanças realizadas.

# English
1) Before changing the image, it is recommended that you save the database data in case you wish to restore it later or in the event of a failure.
- To save the database, execute the following command:
docker exec <postgres_container_name> pg_dump -U <POSTGRES_USER> <database_name> > backup.sql
- The command to restore the database if needed after updating the image is:
docker exec -i <postgres_container_name> psql -U <POSTGRES_USER> -d <database_name> < backup.sql
- If you also want to save the images of your interface, you need to back up Minio (https://min.io/) as well. To do this, simply copy the files from the Minio folder on your machine or use the Minio interface itself.

2) To change the image, you should go to the docker-compose.yml file and find the section for the desired image, for example, 'ui', and replace the repository with the repository of your new image. See the example below:

> ui:
> image: your_new_image_repository:tag

3) After updating the image in the docker-compose.yml file, in order for your application to reflect the changes made in the image, you need to execute the following command:

> docker-compose up -d

4) Check the system health and your new changes.

Referências:

https://reportportal.io/docs/installation-steps/MaintainCommandsCheatSheet

https://min.io/docs/minio/linux/reference/minio-mc.html?ref=docs-redirect#mirror