- La mejor manera que pude hacerlo anda es con el plugin de git
	- Hay que deshabilitar las opciones de git de Control de versiones que viene incorporado con logSeq pero que sino quedan desincronizados
	- Cuando arranca en rojo se puede probar con un pull rebase o un commit
	- Agregué un archivo al gitignore que se modifica cada vez que se abre logseq y que está relacionado con e excalidraw plugin.
	- El commit que Version Control de logseq no ejecuta los hooks, entonces no se pueden usar el precommit y el post commit.
-
- La cagada de esta forma es que no se sincroniza cuando se cierra,
	- Hasta ahora esta es la forma más viable de hacer que ande.
	-
	-
	-
	-
- Prueba usando la version de linux y descomprimida en el directorio .local/share/appl.... parace estar sincronizando.
	- al parecer si hago un cambio, y no lo comiteo, cuando se cierra hace el commit pero no el push
	- si luego de esto vuelvo a abrir y si hacer cambios cierro se hace el push (haría un commit más rápido?)
	  id:: 66fd7210-69b0-4377-9872-1d4aa920319f
	- lo que se me ocurre es que cuando se cierra no le da tiemp a ejecutarse el post commit, entonces no se ejecuta para nada
-
- A veces anda, a veces no. Puede ser que este tardado mucho el Push?!
-