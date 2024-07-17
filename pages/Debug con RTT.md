- Muchas veces es preferible no hacer lo que se hace en un programa común deponer breakpoints por que en general rmpen tanto que no se puede verr el problema. Lo que se suele hacer es loggear valores por usb con **real time transfer** o **RTT** #rtt-target
	- `rtt-target` es un crate que tiene un par de macors que funcionan pareciido al println para mandar datos al host.
	- es necesario habilitarlo en el `Embed.toml` agregando
	  ```toml
	  [default.rtt]
	  enabled=true
	  ```
- Este crate necesita un feature del crate #cortex-m que se llama `critical-section-single-core`. Esto lo agregamos con cargo con el comando `cargo add cortex-m --features critical-section-single-core`, luego podemos agregar `cargo add rtt-target` [[cortex-m]]