# Práctica Metagenómica
Repositorio creado con el objetivo de tener organizados los archivos y flujos de trabajo a usar para el análisis del metagenoma híbrido del suelo marítimo antártico PRJNA681475.

Se utilizará el flujo de trabajo nf-core/mag para el ensamblaje, anotación y análisis de metagenomas. Este será ejecutado en el sistema de flujo de trabajos científicos Nextflow. 

## Antes de iniciar
Debemos descargar antes los envs conda `entrez-direct`, `nextflow`, `sra-tools` 

## Primer paso - descarga de datos del proyecto PRJNA681475
El proyecto PRJNA681475 se encuentra alojado en el National Center for Biotechnology Information (NCBI) como un BioProject. Dentro del BioProject podemos encontrar información agrupada de metadatos, secuencias crudas depositadas en el Sequence Read Archive (SRA), datos ensamblados y anotados, publicaciones relacionadas. 

De la página del BioProject, necesitaremos buscar y descargar información la base de datos SRA. Será necesaria para extraer la lista de identificadores SRR que utilizaremos para descargar luego las secuencias crudas. El archivo **search_SRR_to_list.txt** contiene el script de bash para realizar esta tarea. No olvidar cargar `conda activate entrez-direct`

Al terminar la ejecución del script, tendremos un archivo **.txt** con la lista de identificadores.

## Segundo paso - descargar SRR de la lista
Ya teniendo la lista de SRR creada, se podrán descargar cada una de ellas. Estos archivos SRR tienen la secuenciación de cada muestra de suelo tomada. El archivo **download_SRR_from_list.txt** contiene el script de bash para realizar esta tarea. No olvidar cargar `conda activate sra-tools`

Al terminar la ejecución del script, tendremos una carpeta llamada **lecturas_PRJNA681475** en donde estarán descargados los archivos SRR. 

## Tercer paso - creación del archivo de entrada
Luego de descargar los archivos SRR y tenerlos almacenados en una misma carpeta, crearemos el archivo de entrada que será utilizado por el flujo de trabajo de nf-core/mag. El archivo tendrá los nombres de las muestras, el grupo, lecturas cortas, lecturas largas y plataformas de secuenciación. El encabezado de la tabla, con ejemplos de lecturas largas y cortas, luce de la siguiente forma: 

| sample | group | short_reads_1 | short_reads_2 | long_reads | short_reads_platform | long_reads_platform |
|-----------|-------|---------------|---------------|------------|----------------------|----------------------|
| MA-1_illumina | 1 | ./lecturas_PRJNA681475/SRR13165308_1.fastq.gz   | ./lecturas_PRJNA681475/SRR13165308_2.fastq.gz   |  | ILLUMINA             |             |
| MA-1_nanopore_run1 | 2 |    |    | ./lecturas_PRJNA681475/SRR18260858.fastq.gz |               |OXFORD_NANOPORE               |

El archivo será nombrado **samplesheet.csv**, se encuentra delimitado por comas. 

## Cuarto paso - iniciar flujo de trabajo de nf-core/mag en Nextflow
Con el archivo de entrada generado, iniciamos la ejecución del flujo de trabajo con el siguiente código escrito en Bash. No olvidar cargar `conda activate nextflow `

```console
run nf-core/mag --input samplesheet.csv --outdir resultados_nf-coremag -profile docker
```

o también se puede crear un archivo `YAML` que contenga

```
input: './samplesheet.csv'
outdir: './resultados_nf-coremag/'
<...>
```

y se utilizaría el siguiente código escrito en Bash:

```console
nextflow run nf-core/mag -profile docker -params-file params.yaml
```

Al iniciar la ejecución del flujo de trabajo, las siguientes carpetas se crearán en el directorio de trabajo:



- **work**:              directorio que contiene los archivos de trabajo de nextflow
- **resultados_nf-coremag**:              resultados terminados en la ubicación indicada (definida con --outdir)
- **.nextflow_log**:         archivo Log de Nextflow
- Otros archivos ocultos de nextflow, eg. historial de ejecuciones del flujo de trabajo y logs antiguos.

