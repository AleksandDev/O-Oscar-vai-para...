# O-Oscar-vai-para...
# Nomeados ao Oscar

Contém a base de indicados ao Oscar em formato JSON para treinar comandos de consulta no MongoDB. 

* Quantas vezes Natalie Portman foi indicada ao Oscar?

R: 3 vezes

Q:
```sql
SELECT COUNT(*) FROM indicados WHERE "Name" Like "%Natalie Portman%";
```

* Quantos Oscars Natalie Portman ganhou?

* Amy Adams já ganhou algum Oscar?
R:0
 SELECT * FROM indicados_ao_oscar WHERE nome_do_indicado LIKE '%adams%' and vencedor=true;

* A série de filmes Toy Story ganhou um Oscar em quais anos?
R: 2011 e 2020
 SELECT * FROM indicados_ao_oscar WHERE nome_do_filme LIKE '%Toy Story%' and vencedor="true";
* A partir de que ano que a categoria "Actress" deixa de existir? 

* Quem ganhou o primeiro Oscar para Melhor Atriz? Em que ano?
R: em 1976
SELECT * FROM indicados_ao_oscar WHERE categoria = "Actress" order by ano_cerimonia desc;

* Na campo "Vencedor", altere todos os valores com "true" para 1 e todos os valores "false" para 0.
R: feito
UPDATE indicados_ao_oscar SET vencedor = "1" WHERE vencedor = "true";
UPDATE indicados_ao_oscar SET vencedor = "0" WHERE vencedor = "false";

* Em qual edição do Oscar "Crash" concorreu ao Oscar?
R: 78
SELECT * FROM indicados_ao_oscar WHERE nome_do_filme LIKE "Crash" 

* O filme Central do Brasil aparece no Oscar?
R: sim, nao ganhou nenhum
SELECT * FROM indicados_ao_oscar WHERE nome_do_filme LIKE "Central Station" ;

* Inclua no banco 3 filmes que nunca foram nem nomeados ao Oscar, mas que merecem ser. 
INSERT INTO indicados_ao_oscar(ano_filmagem,ano_cerimonia,cerimonia,categoria,nome_do_indicado,nome_do_filme,vencedor) VALUES (2004,2005,1,'Best Picture','Eric, J. Mackye','The Butterfly Effect','1');
INSERT INTO indicados_ao_oscar(ano_filmagem,ano_cerimonia,cerimonia,categoria,nome_do_indicado,nome_do_filme,vencedor) VALUES (1994,1995,1,'Best Picture','Luc Besson','Léon','1');
INSERT INTO indicados_ao_oscar(ano_filmagem,ano_cerimonia,cerimonia,categoria,nome_do_indicado,nome_do_filme,vencedor) VALUES (2001,2002,1,'Best Picture','Richard Kelly','Donnie Darko','1');

* Denzel Washington já ganhou algum Oscar?
R: ganhou 2
 SELECT * FROM indicados_ao_oscar WHERE nome_do_indicado LIKE "Denzel Washington" and vencedor = "1" ;

* Quais os filmes que ganharam o Oscar de Melhor Filme?
R: muito, Lawrence of Arabia, My Fair Lady, A Man for All Seasons entre outros.
 SELECT * FROM indicados_ao_oscar WHERE categoria = "best picture" and vencedor = "1"  ;
 
* Bonus: Quais os filmes que ganharam o Oscar de Melhor Filme e Melhor Diretor na mesma cerimonia?
R: muitos
select nome_do_filme, ano_cerimonia, vencedor
from indicados_ao_oscar
where categoria in ("Best Picture", "Directing") 
AND vencedor = 'True'

GROUP BY nome_do_filme, ano_cerimonia
HAVING COUNT (DISTINCT categoria) =  1
order by ano_cerimonia desc;

* Bonus: Denzel Washington e Jamie Foxx já concorreram ao Oscar no mesmo ano?
R: não 
select nome_do_filme, nome_do_indicado, ano_cerimonia, vencedor
from indicados_ao_oscar
where nome_do_indicado in ("Denzel Washington", "Jamie Foxx")
group by nome_do_filme, nome_do_indicado, ano_cerimonia, vencedor 
order by ano_cerimonia desc;
