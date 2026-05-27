# Practica Metagenómica
Repositorio creado con el objetivo de tener organizados los archivos y flujos de trabajo a usar para el análisis del metagenoma híbrido del suelo marítimo antártico PRJNA681475.

Se utilizará el flujo de trabajo nf-core/mag para el ensamblaje, aanotación y análisis de metagenomas. Este será ejecutado en el sistema de flujo de trabajos científicos Nextflow. 

## Antes de iniciar
Debemos descargar antes los envs conda `entrez-direct` `nextflow` 

## Primer paso - descarga de datos del proyecto PRJNA681475
El proyecto PRJNA681475 se encuentra alojado en el National Center for Biotechnology Information (NCBI) como un BioProject. Dentro del BioProject podemos encontrar información agrupada de metadatos, secuencias crudas depositadas en el Sequence Read Archive (SRA), datos ensamblados y anotados, publicaciones relacionadas. 

De la página del BioProject, necesitaremos buscar y descargar información la base de datos SRA. Será necesaria para extraer la lista de identificadores SRR que utilizaremos para descargar luego las secuencias crudas. El archivo **search_SRR_to_list.txt** contiene el script de bash para realizar esta tarea.

Al terminar la ejecución del script, tendremos un archivo **.txt** con la lista de identificadores.

## Segundo paso - descargar SRR de la lista
Ya teniendo la lista de SRR creada, se podrán descargar 


