1- Quantas vezes Natalie Portman foi indicada ao Oscar?
resposta > 3
db.registros.countDocuments({nome_do_indicado:{$regex:"Natalie Portman", $options: "i"}})


2- Quantos Oscars Natalie Portman ganhou?
ganhou 1 
db.registros.countDocuments({nome_do_indicado: "Natalie Portman", vencedor: "true"})

3- Amy Adams já ganhou algum Oscar?
não Amy Adams não ganhou nenhum Oscar.
db.registros.countDocuments({nome_do_indicado: "Amy Adams", vencedor: "true"})


4- A série de filmes Toy Story ganhou um Oscar em quais anos?
Toy Story 3 em 2011 ganhou dois Oscars e em 2020 Toy story 4 ganhou mais um 


5- A partir de que ano que a categoria "Actress" deixa de existir?
 

6- O primeiro Oscar para melhor Atriz foi para quem? Em que ano?

7- Na campo "Vencedor", altere todos os valores com "Sim" para 1 e todos os valores "Não" para 0.

8- Em qual edição do Oscar "Crash" concorreu ao Oscar?

9- Bom... dê um Oscar para um filme que merece muito, mas não ganhou.

10- O filme Central do Brasil aparece no Oscar?

11- Inclua no banco 3 filmes que nunca foram nem nomeados ao Oscar, mas que merecem ser. 

14 - Pensando no ano em que você nasceu: Qual foi o Oscar de melhor filme, Melhor Atriz e Melhor Diretor?