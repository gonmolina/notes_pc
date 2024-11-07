## Webdiagram
- El webdiagram:
	- el servidor web es el encargado de:
	  id:: 672d0480-c045-4a3a-8966-cddb0bcee83f
		- atender los reuqest desde los clientes web 
		  id:: 672d0542-9f78-44e7-a9ba-9187bec13a89
		- pedir al servidos de simulaciones que simule, cree las instancias de simulación, etc.
		- la configuración se encuentra dentro de la carpera webduagram en el archivo config.json
		  id:: 672d0653-1bab-44fd-9830-0108bc1b0cad
			- en mi cimoutadora estoy usando el python de sistema 3.10, ubuntu 20.04, con el siguiente comando
			  id:: 672d0682-806c-4c77-b573-a80927911752
				- id:: 672d07ae-b380-4269-8f16-3461ea7acb01
				  ```bash
				  /bin/python webdiagram.py
				  ```
	- el servidor de simulación:
		- gestiona kas simulaciones y comunicación de variables.
		  id:: 672d05a5-2a4c-4cc7-b2e8-3f9a69353129
			- para hacerlo andar tengo que ejecutar el siguiente comando:
			- ```bash
			  ./build/src/server -m mongodb://pallasUSER:peql1234@10.73.32.33/test -db pallas -h 0.0.0.0
			  ```
			- lo tengo que ejecutar de forma de ver el archivo server en la ubicacion que estoy buscando
- ## arquitectura
- Para la arquitectura ejecutar el bat que se corresponde al modo de desarrollo
	- usuario y password devel 
	  id:: 672d0936-d250-4fd6-977f-603ec5ad5d98
	- hay que generar el modulo para ejecucion,
		- yo lo veo como una especie de configuración de instancia
		- para configurar el modulo de webdiagram hay que poner:
			- un nombre a la configuracion (a mi configuración le puse gonza)
			- En host hay que poner la dirección de la máquina donde corre el webdiagram con protocolo ws y puerto 8001, es decir ws://10.73.32.988:80001
			  id:: 672d0a43-b222-473f-ba44-38ed4290b572
			- En instance name pones el nombre de usuario para generar las instancias en webdiagram al vuelo. De esta manera el modulo usa la instancia creada acutal por el usurio. Si se usa esta configuración se debe dejar vacio el instance config
			- si se llena el instance confug usa una de las configuraciones de operación guardadas
		-
-
-