# Pokémon

Há mais de 10 anos, crianças do mundo inteiro vêm descobrindo o mundo encantado dos Pokémon. Hoje, a família de produtos Pokémon inclui videogames, o jogo Pokémon Estampas Ilustradas, a série de TV animada, filmes, brinquedos e muito mais. Muitos pais acreditam que o Pokémon Estampas Ilustradas e os videogames do Pokémon estimulam seus filhos a aprender a ler, já que a leitura é indispensável na maioria dos jogos do Pokémon. Os jogos também estimulam o pensamento estratégico e, em muitos casos, habilidades matemáticas básicas. O Pokémon valoriza muito o espírito esportivo e o respeito pelos outros jogadores.

## O que são Pokémon?

Pokémon são criaturas de todas as formas e tamanhos que convivem com os humanos na natureza. Na grande maioria, os Pokémon não falam, exceto para proferir seus nomes. Os Pokémon são criados e comandados por seus donos (os chamados "Treinadores"). No decorrer das aventuras, os Pokémon crescem e ganham experiência, podendo até mesmo evoluir para Pokémon mais fortes. Alguns Pokémon, como Pikachu, Piplup e Charizard, possuem papéis de destaque na série de videogames, no jogo Estampas Ilustradas e nos programas de TV, mas eles são apenas algumas das quase 500 criaturas que habitam o universo dos Pokémon.

**Fonte:** [Webiste Oficial - Pokémon](https://www.pokemon.com/br/guia-para-pais/)


## Ponto de Partida

Para começar esse exercício, você deverá: 

* 1. Pegar o arquivo `pokedex_create_v1.sql`, disponível na pasta [data](data/)
* 2. Abrir o software [MySQL](https://www.mysql.com/products/workbench/)
* 3. Exectuar o script para importar um novo banco de dados 


## Resumo do Projeto

Para este projeto, sua tarefa é criar consultas (queries), usando as técnicas da [Linguagem de Consulta de Dados](https://github.com/profdiegoaugusto/banco-dados/tree/master/mysql/linguagem-consulta-dados) no banco de dados `pokedex` do universo Pokémon. O esquema do banco de dados possui apenas uma tabela chamada `Pokémon`, com as seguintes colunas:

| Coluna          | Descrição                                                                                                                                                                                                                        |
|-----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| numero          | Chave Primária: o número do Pokémon no Pokedex Nacional                                                                                                                                                                          |
| nome            | Nome do Pokémon                                                                                                                                                                                                                  |
| tipo1           | Todas as criaturas Pokémon e seus movimentos recebem determinados tipos. Cada tipo tem vários pontos fortes e fracos no ataque e na defesa, ou seja, cada Pokémon tem um tipo que determina sua fraqueza/resistência aos ataques |
| tipo2           | O tipo secundário do Pokémon caso ele possua                                                                                                                                                                                     |
| total           | Soma de todas as estatísticas básicas (Pontos de Vida, Ataque, Defesa, Ataque Especial, Defesa Especial e Velocidade)                                                                                                            |
| hp              | HP (Hit Points ou Health Points), define quanto dano um Pokémon pode suportar antes de desmaiar                                                                                                                                  |
| ataque          | O ataque base do Pokémon                                                                                                                                                                                                         |
| defesa          | A defesa base do Pokémon                                                                                                                                                                                                         |
| ataque_especial | O ataque especial base do Pokémon                                                                                                                                                                                                |
| defesa_especial | A defesa especial base do Pokémon                                                                                                                                                                                                |
| velocidade      | A velocidade base do Pokémon                                                                                                                                                                                                     |
| geracao         | Número da geração em que o Pokémon foi introduzido                                                                                                                                                                               |
| lendario        | Valor Booleano que indica se o Pokémon é lendário ou não                                                                                                                                                                         |
| cor             | A cor do Pokémon                                                                                                                                                                                                                 |
| altura_m        | Altura em metros do Pokémon                                                                                                                                                                                                      |
| peso_kg         | Peso em Kilos do Pokémon                                                                                                                                                                                                         |
| taxa_captura | A taxa de captura do Pokémon é um número entre 0 e 255, quanto maior, melhor |


## Consultas

1. Selecione o banco de dados (esquema) `pokédex`.
```sql
USE pokedex;
```

2. Obtenha informações da estrutura da tabela `Pokémon`.

```sql
FROM
	information_schema.TABLES
WHERE
	TABLE_SCHEMA = 'pokedex'
	 AND TABLE_NAME = 'Pokemon'
;
```

3. Selecione todos os pokémons cadastrados no banco de dados.

```sql
USE pokedex;

SELECT
	*
FROM
	Pokemon
;
```

4. Selecione o `numero`, `nome`, `cor`, `altura_m` e `peso_kg` de todos os pokémons cadastrados.

```sql
USE pokedex;

SELECT
	numero,
	nome,
	cor,
	altura_m,
	peso_kg
FROM
	Pokemon
;
```

5. Qual é o `numero` e o `nome` de todos os pokémons da primeira geração?

```sql
USE pokedex;

SELECT
	numero,
	nome
FROM
	Pokemon
WHERE geracao = 1
;
```

6. Quais são os pokémons `Amarelo` da primeira geração?

```sql
USE pokedex;

SELECT
	*
FROM
	Pokemon
WHERE
	geracao = 1
	 AND cor = 'Amarelo'
;
```

7. Qual é o pokémon mais forte?

```sql
USE pokedex;

SELECT
	*
FROM
	Pokemon
ORDER BY total DESC
LIMIT 1
;
```


8. Selecione o `numero`, `nome` e `tipo1`; de todos os pokémons cujo tipo primário é `Fire`.

```sql
USE pokedex;

SELECT
	numero,
	nome,
	tipo1
FROM
	Pokemon
WHERE
	tipo1 = 'Fire'
;
```

10. Selecione em ordem decrescente o `numero`, `nome` e `defesa` de todos os pokémons.

```sql
USE pokedex;

SELECT
	numero,
	nome,
	defesa
FROM
	Pokemon
ORDER BY defesa DESC
;
```


11. Qual o pokémon possui *menor* taxa de captura? Selecione apenas `numero` e `nome`.

```sql
USE pokedex;

SELECT
	numero,
	nome
FROM
	Pokemon
ORDER BY taxa_captura ASC
LIMIT 1
;
```


12. Selecione todos pokémons que não possuem tipo secundário, ou seja, `tipo2`.

```sql
USE pokedex;

SELECT
	*
FROM
	Pokemon
WHERE
	tipo2 IS NULL
;
```

13. Selecione `numero`, `nome`, `tipo1`, `tipo2` de todos os pokémons que possuem o peso entre 100kg e 500kg.

```sql
USE pokedex;

SELECT
	numero,
	nome,
	tipo1,
	tipo2
FROM
	Pokemon
WHERE
	peso_kg > 100 AND peso_kg < 500
;
```


14. Crie um ranking dos top 10 pokémons mais velozes, contendo `numero`, `nome` e `velocidade`.

```sql
USE pokedex;

SELECT
	numero,
	nome,
	velocidade
FROM
	Pokemon
ORDER BY velocidade DESC
LIMIT 10
;
``` 


15. Selecione `numero`, `nome`, `tipo1`, `tipo2`, `taxa_captura` dos pokémons que possuem os dois tipos e tenham uma taxa de captura acima de 100. Ordene os resultados decrescente pela taxa de captura.

```sql
USE pokedex;

SELECT
	numero,
	nome,
	tipo1,
	tipo2,
	taxa_captura
FROM
	Pokemon
WHERE
	taxa_captura > 100
	 AND tipo2 IS NOT NULL
ORDER BY taxa_captura DESC
;
```

16. Quais são os tipos primários dos pokémons?

```sql
USE pokedex;

SELECT
	tipo1
FROM
	Pokemon
GROUP BY
	tipo1
;
```

17. Selecione o `numero`, `nome` e `cor`; de todos os pokémons que o nome começa com a letra `D`.

```sql
USE pokedex;

SELECT
	numero,
	nome,
	cor
FROM
	Pokemon
WHERE
	nome LIKE 'D%'
;
```

18. Qual é o pokémon mais poderoso de todas as gerações?

```sql
USE pokedex;

SELECT
	*
FROM
	Pokemon
ORDER BY total DESC
LIMIT 1
;
```

19. Selecione o `numero`, `nome`, `defesa`, `ataque` dos pokémons com defesa > 60 e ataque <= 70; ordenados decrescente pelo `total`. 

```sql
USE pokedex;

SELECT
	numero,
	nome,
	defesa,
	ataque
FROM
	Pokemon
WHERE
	defesa > 60
		AND ataque <= 70
ORDER BY total DESC
;
```

20. Selecione todos os pokémons do tipo `Planta` e `Venenoso` que não sejam `Green`, ordenado crescente pelo `nome`.

```sql
USE pokedex;

SELECT
	*
FROM
	Pokemon
WHERE
	cor != 'Green'
		AND tipo1 LIKE 'Planta'
		AND tipo2 LIKE 'Venenoso'
ORDER BY nome ASC
;
```

21. Selecione de maneira crescente os nomes dos pokémons que possuem a letra y na 4ª posição do nome.

```sql
USE pokedex;

SELECT
	*
FROM
	Pokemon
WHERE
	nome LIKE '____Y'
ORDER BY nome ASC
;
```

22. Qual é o maior valor de `ataque_especial` cadastrado?

```sql
USE pokedex;

SELECT
	MAX(ataque_especial)
FROM
	Pokemon
;
```

23. Selecione o `numero`, `nome` e `altura_m` dos pokémons que possuem altura acima de 2,10m.

```sql
USE pokedex;

SELECT
	numero,
	nome,
	altura_m
FROM
	Pokemon
WHERE
	altura_m > 2.1
;
```

24. Quais são as diferentes tipos de cores dos pokémons? Apresente os resultados de maneira crescente pelo nome da cor.

```sql
USE pokedex;

SELECT
	cor
FROM
	Pokemon
GROUP BY cor
ORDER BY cor ASC
;
```

25. Selecione o `nome` e `velocidade` dos pokémons com velocidade entre 30 e 70. Ordene os resultados por nome (crescente) e velocidade (decrescente)

```sql
USE pokedex;

SELECT
	nome,
	velocidade
FROM
	Pokemon
WHERE
	velocidade > 30 AND velocidade < 70
ORDER BY
	nome ASC,
	velocidade DESC
;
```

26. Quem são os pokémons lendários? Apresente os resultados ordenados por `total` decrescente.

```sql
USE pokedex;

SELECT
	*
FROM
	Pokemon
WHERE
	lendario = 1
ORDER BY total DESC
;
```


27. Selecione os pokémons da primeira geração com taxa de captura igual a 255.

```sql
USE pokedex;

SELECT
	*
FROM
	Pokemon
WHERE
	geracao = 1
		AND taxa_captura = 255
ORDER BY total DESC
;
```


28. Quem é o mais poderoso? selecione o `Pikachu`, `Squirtle`, `Bulbasaur` e `Charmander`; ordenados decrescente pelo `total`. 

```sql
USE pokedex;

SELECT
	*
FROM
	Pokemon
WHERE
	nome IN (
		'Pikachu',
		'Squirtle',
		'Bulbasaur',
		'Charmander'
	)
ORDER BY total DESC
;
```

29. Quem são os pokémons da primeira geração, que começam com a letra `d` e não possuem tipo secundário?
Ordene os resultados crescente por `taxa_captura` e decrescente pelo `total`.

```sql
USE pokedex;

SELECT
	*
FROM
	Pokemon
WHERE
	geracao = 1
	 AND nome LIKE 'D%'
	 AND tipo2 IS NULL
ORDER BY
	taxa_captura ASC,
	total DESC
;
```

30. Qual é o ranking dos top 5 pokémons lendários com maior `taxa_captura` e `total`? Apresente apenas `numero, nome, total, taxa_captura` nos resultados.

```sql
USE pokedex;

SELECT
	numero,
	nome,
	total,
	taxa_captura
FROM
	Pokemon
WHERE
	lendario = 1
ORDER BY
	taxa_captura DESC,
	total DESC
LIMIT 5
;
```

31. Selecione o `numero`, `nome`, `peso_kg` dos pokémons com peso entre 2kg e 3kgs?

```sql
USE pokedex;

SELECT
	numero,
	nome,
	peso_kg
FROM
	Pokemon
WHERE
	peso_kg > 2 AND peso_kg < 3
;
```

32. Selecione o `numero`, `nome`, `tipo1` e `tipo2` dos pokémons com tipo primário `Normal`, que não possuem tipo secundário. Existe algum pokémon lendário nos resultados, se sim, os remova dos resultados?

```sql
USE pokedex;

SELECT
	numero,
	nome,
	tipo1,
	tipo2
FROM
	Pokemon
WHERE
	tipo1 LIKE 'Normal'
		AND tipo2 IS NULL
		AND lendario = 0
;
```

33. Quem são os pokémons do tipo `Water` que não são azuis? Apresente `numero`, `nome`, `tipo1`, `tipo2` e `cor`, ordenados pelo `nome` de maneira crescente.

```sql
USE pokedex;

SELECT
	numero,
	nome,
	tipo1,
	tipo2,
	cor
FROM
	Pokemon
WHERE
	tipo1 LIKE 'Water'
		AND COR != 'Blue'
ORDER BY nome ASC
;
```

34. Crie um ranking dos top 10 pokémons mais lentos.

```sql
USE pokedex;

SELECT
	*
FROM
	Pokemon
ORDER BY velocidade ASC
LIMIT 10
;
```

35. Selecione os pokémons cujo nome comece e termine com a letra `a`. 

```sql
USE pokedex;

SELECT
	*
FROM
	Pokemon
WHERE
	nome LIKE 'A%a'
;
```

36. Quem são os pokémons do tipo `Fire` que não são vermelhos? Apresente `numero`, `nome`, `tipo1`, `tipo2` e `cor`, ordenados pelo `nome` de maneira crescente.

```sql
USE pokedex;

SELECT
	numero,
	nome,
	tipo1,
	tipo2,
	cor
FROM
	Pokemon
WHERE
	tipo1 LIKE 'Fire'
		AND COR != 'Red'
ORDER BY nome ASC
;
```

37. Quais são os diferentes tipos de `peso_kg` dos pokémons? Apresente os resultados ordenados de maneira crescente.

```sql
USE pokedex;

SELECT
	peso_kg
FROM
	Pokemon
GROUP BY peso_kg
ORDER BY peso_kg ASC
;
```

38. Selecione o `numero`, `nome` e `hp` dos pokémons com valores entre 0 e 100. Ordene os resultados de maneira crescente por `hp` e `nome`.

```sql
USE pokedex;

SELECT
	numero,
	nome,
	hp
FROM
	Pokemon
WHERE
	hp > 0 AND hp < 100
ORDER BY
	hp ASC,
	nome ASC
;
```

39. Selecione o `numero`, `nome`, `hp`, `ataque`, `defesa` e `total`; dos pokémons com valores de `hp`, `ataque`, `defesa` maiores ou iguais a 100.

```sql
USE pokedex;

SELECT
	numero,
	nome,
	hp,
	ataque,
	defesa,
	total
FROM
	Pokemon
WHERE
	hp >= 100
		AND ataque >= 100
		AND defesa >= 100
;
```

40. Selecione todos os pokémons do tipos `Water` e `Gelo`, ordenados decrescente por `total`.

```sql
USE pokedex;

SELECT
	*
FROM
	Pokemon
WHERE
	tipo1 LIKE 'Water'
		AND tipo2 LIKE 'Gelo'
GROUP BY numero
ORDER  BY total DESC
;
```


## REFERÊNCIAS

* [Webiste Oficial - Pokémon](https://www.pokemon.com/br/guia-para-pais/)
* [Guia de Estilo SQL · SQL Style Guide](https://www.sqlstyle.guide/pt-br/)







