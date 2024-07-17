- Lo primero que tenemos que hacer es instalar #rustup para poder instalar los toolchain de los micros.
- Un editor "rust rover", #neovim o #vscode.
- Averiguar que micro vamos a estar programando.
	- necesitamos saber con claridad que familia de cortex es y en base a eso que compilador vamos a usar. recomeinda un nordi. yo voy a usar un stm32.
	- El compilador tiene el nombre siguiendo el siguiente esquema:
		- <arch><sub>-vendor-<sys>-<env>
			- arch = x86_64, i386, arm, ...
			- sub = v4, v5, v5 (para los arm por ejemplo)
			- [optional] pc, apple, ibm, ...
			- sys = none, linux, win32, darwin, ...
			- env = eabi, gnu, elf, ..
	- Pasa saber que compilador tenemos que ver la arquitectura. Por ejemple el STM32F4 es Cortex M3 y tiene un porcesador numérico.
	- Para ese procesador necesitamossaber su arquitectura. para nuestro caso es 	Armv7E-M. Entonces en rustup buscamos el compilador para esa arquitectura. 
	  Vemos que es https://doc.rust-lang.org/nightly/rustc/platform-support/thumbv7em-none-eabi.html (tiene procesador de punto flotante, por que sería eabihf)
	- Se debe instalar #rustup
		- #rustup show nos muestra los toolchains instalados
		- `rustup add thumbv7em-none-eabihf`
		- para iniciar un proyecto se hace igual que uno comun con `cargo new nombre-del-proyecto`
	-
	- Una vez iniciado el proyecto tenemos algo de boilerplate:
		- quitar la librería standard `#![no_std]`
		- no usar la función main `#![no_main]`
		  id:: 6673908e-6d92-4b15-8618-f0e23515afc2
	- Las dependencias se manejan con cargo como con cualquier proyecto con #cargo
	- La primer dependecia nos sirve, entre otras cosas, para poder ubicar nuestro programa corrrectamente en la memoria del microcontrlador
		- la primer depedencia que usaremos es `cortex-m-rt`: este crate usa el archivo `memory.x` para saber donde escribir en la memoria. Tenemos que buscar en el manual como es el mapa de memoria de nuestro dispositivo.
	- `#[entry]`  le decimos que función es el punto de entrada del micro. La función de entrada no retorna nunca y eso de dice `fn main -> !`
	- para simplificar el proceso de compilación se hace un archivo de configuración de `.cargo\config.toml`:
	- id:: 66739870-956c-41e9-a12a-b5f1a357227f
	  ```toml
	  [build]
	  target = "thumbv7em-none-eabihf"
	  
	  [target.thumbv7em-none-eabihf]
	  rustflags = ["-C", "link-arg=-Tlink.x"]
	  ```
	- Es importante configurar #rust-analyzer para que sepa que estamos compilando para otro target.
		- ```json
		  {
		  "rust-analyzer.check.allTargets": false,
		  "rust-analyzer.cargo.target: "thumbv7em-none-eabihf",
		  }
		  ```
	-
	- Es necesario agregar el `panic-handler`.  Para esto se agrega un crate que se llama `panic_halt`, que son 13 lineas de código, pero que soluciona el problema. Lo agregamos con  `cargo add panic_hallt`.
	  id:: 66739b03-2cc5-46e7-b2f5-16e69a959f08
	- Ahora ya podemos compilar el proyecto. Obviamente si no hay nada en rojo marcado por el LSP.
	- Si copilamos correctamente entonces ahora podemos analizar que tiene el binario. Para esto podemos usar dos utilidades:
		- `llvm-tools` se instala con `rustup component add llvm-tools` #rustup
		  id:: 66739d85-bf6f-4032-b8d5-882aec0a08c0
		- y una utilidad para analizar los binarios que se llama `cargo-binutils`, que funciona como subcomando de cargo, y e instala con `cargo install cargo-binutils`.
	- Para usar `cargo-binutils` lo  unico que tenemos que hacer es usa con cargo el comando de llvm-tools que queremos usar, por ejemplo:
		- `cargo size -- -Ax`
	- Para flasher la memoria se utiliza programa de cargo que se llama `cargo-embed`. #cargo-embed
		- con `cargo embed --help` vemos la ayuda
		- com `cargo embed --list-chips`podemos ver que chips están soportados, podemos pipear al grep para buscar nuestro chip con `cargo embed --chip nombre-del-chip` mandamos el programa al chip.
	- Para eviar tener que poner esa linea larga cada vez qeu queremos manda un programa al chip podemos hacer un archivo `Embed.toml` #embed.toml
		- ```toml
		  [default.general]
		  chip = "nombre-del-chip"
		  ```
		- Ahora con `cargo embed` va a mandar el programa al chip.
	- Finalmente  #Debug
		- {{embed [[Debug con RTT]]}}
		- {{embed [[Embed Debug con GDB]]}}
	-