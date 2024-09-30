<h1>Atividade Momentos</h1>

<h2>1. Quantos funcionários da empresa Momento trabalham no departamento de vendas?</h2>
<p>10 funcionários estão nesse departamento.</p>
<pre><code>
db.funcionarios.countDocuments({departamento:ObjectId("85992103f9b3e0b3b3c1fe71")})
</code></pre>

<h2>2. Inclua suas próprias informações no departamento de Tecnologia da empresa.</h2>
<pre><code>
db.tecnologia.insertMany([
    {
        nome: "kauan lusbel caetano freitas",
        telefone: "11-913190349",
        email: "lusbelk@gmail.com",
        dataAdmissao: "15/02/2024",
        cargo: "Full stack",
        salario: 5000,
        departamento: ObjectId('5f8b3f3f9b3e0b3b3c1e3e3e')
    },
    {
        nome: "murilo",
        telefone: "11-999999999",
        email: "outroemail@gmail.com",
        dataAdmissao: "10/03/2024",
        cargo: "Backend",
        salario: 4500,
        departamento: ObjectId('5f8b3f3f9b3e0b3b3c1e3e3e')
    }
]);
</code></pre>

<h2>3. Quantos funcionários temos ao total na empresa?</h2>
<p>23 funcionários.</p>
<pre><code>
db.funcionarios.countDocuments()
</code></pre>

<h2>4. Quantos funcionários estão no Departamento de Tecnologia?</h2>
<p>6 funcionários.</p>
<pre><code>
db.funcionarios.countDocuments({departamento: ObjectId('85992103f9b3e0b3b3c1fe74')})
</code></pre>

<h2>5. Qual a média salarial do departamento de Tecnologia?</h2>
<p>A soma dos salários de 5 funcionários é 22800.</p>
<pre><code>
db.funcionarios.aggregate([{
$match:{departamento: ObjectId('85992103f9b3e0b3b3c1fe74')}
},
{
$group:{   
_id: 0 ,
soma_salario: {$sum: "$salario"},
somafun: {$sum:1}
}
}
])
</code></pre>

<h2>6. Quanto o departamento de Vendas gasta em salários?</h2>
<p>O departamento de Vendas gasta 95100 em salários.</p>
<pre><code>
db.funcionarios.aggregate([{
$match:{departamento:ObjectId("85992103f9b3e0b3b3c1fe71")}
},
{
$group:{
_id: 0,
soma:{$sum:"$salario"},
somafun:{$sum:1}
}
}
])
</code></pre>

<h2>7. Um novo departamento foi criado: Inovações</h2>
<p>O departamento de Inovações será locado no Brasil. Incluindo-o no banco de dados da empresa:</p>
<pre><code>
db.departamentos.insertOne({
'nome':'inovações',
'escritorio':ObjectId()
})
</code></pre>

<h2>8. Inclua alguns colegas de turma no Departamento de Inovações.</h2>
<pre><code>
db.funcionarios.insertMany([{
'nome':'kaue caetano',
'telefone':'11 945872562',
'email':'caetanoka@gmail.com',
'cargo': 'frontend',
'salario':'35000',
'departamento':ObjectId('66fae0d1d9a9e8ffbb9fac8c')
}])

db.funcionarios.insertMany([{
'nome':'hudson',
'telefone':'11 25619932',
'email':'hudsonpalmeira@gmail.com',
'cargo': 'frontend',
'salario':'5000',
'departamento':ObjectId('66fae0d1d9a9e8ffbb9fac8c')
}])
</code></pre>

<h2>9. Quantos funcionários a empresa Momento tem agora?</h2>
<p>A empresa está com 27 funcionários.</p>
<pre><code>
db.funcionarios.countDocuments()
</code></pre>

<h2>10. Quantos funcionários da empresa possuem cônjuges?</h2>
<p>7 funcionários possuem cônjuges.</p>
<pre><code>
db.funcionarios.countDocuments({"dependentes.conjuge":{$exists: true}})
</code></pre>

<h2>11. Qual a média salarial dos funcionários da empresa, excluindo-se o CEO?</h2>
<pre><code>
db.funcionarios.aggregate([{
$match:{cargo:{$ne:'CEO'}}
},
{
$group:{   
_id: 0 ,
soma_salario: {$sum: "$salario"},
somafun: {$sum:1}
}
},
{
$project:{
_id: null,
calculo: {$divide:['$soma_salario','$somafun'] }
}
}
])
</code></pre>
<p>Resultado: 8587.2</p>

<h2>12. Qual o departamento com a maior média salarial?</h2>
<p>O departamento com a maior média salarial é o Executivo.</p>
<pre><code>
db.funcionarios.aggregate([{
$group:{ 
_id: '$departamento',
contagem: {$sum:1},
salario_contagem:{$sum:'$salario'}}
},
{
$project:{
calculo:{$divide:['$salario_contagem','$contagem']}
}},                      
{
$sort:{"calculo":-1}
}
])
</code></pre>
<p>Resultado: 71000</p>

<h2>13. Qual o departamento com o menor número de funcionários?</h2>
<p>O departamento Executivo consta apenas com uma pessoa.</p>
<pre><code>
db.funcionarios.aggregate([{
$group:{ 
_id: '$departamento',
contagem: {$sum:1}
}},
{
$sort:{"contagem":1}
},
{
$limit:1
}
])
</code></pre>

<h2>14. Qual o produto mais valioso da empresa?</h2>
<pre><code>
db.vendas.aggregate([{
$sort:{quantidade:1}
},{
$sort:{precoUnitario:-1}
}])
</code></pre>
<p>Resultado: Sabre de Luz (Mace Windu), Preço Unitário: 990.29</p>

<h2>15. Qual o produto mais vendido da empresa?</h2>
<pre><code>
db.vendas.aggregate([{
$sort:{quantidade:-1}},{$limit:1}])
</code></pre>
<p>Resultado: Uniforme de Moléculas Instáveis, Quantidade: 10</p>
