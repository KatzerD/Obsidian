Una entidad pasara ser manejada por el contexto de persistencia cuando esta sea persistida mediante el método persist() del EntityManager, o bien un objeto detached es unido al contexto de persistencia mediante el método merge().

En este punto, la entidad pasara a estar asociada a lo que comúnmente llamamos el contexto de persistencia.

En este caso, y mientras la entidad sea manejada/asociada por el contexto de persistencia (también se las conoce como attached entities) y el estado (valores de las propiedades) de la entidad serán automáticamente sincronizadas con la BD mediante el método flush().

