---
layout:     post
title:      Registro.br e Heroku – Configurando DNS
date:       2012-04-26 10:00:00
summary:    Configurando seu DNS do registr.br para apontar para uma aplicação no Heroku
categories: heroku
---

![heroku](/pixyll/images/2012-04-26-registro-br-e-heroku-configurando-dns/heroku.jpg)

Hoje existem inúmeras plataformas que você pode escolher para hospedar
sua aplicação e inúmeras questões que você deve levar em consideração na
hora de escolher entre uma ou outra. Para isso existe o [heroku](http://www.heroku.com/), uma
ótima alternativa para a maioria das aplicações web e a lista de
justificativas a favor de seu uso é enorme, como por exemplo custo
inicial zero, facilidade de manutenção e gerenciamento de recursos,
[integração com git](https://devcenter.heroku.com/articles/git) tornando o tempo de deploy mínimo, [excelente
documentação](https://devcenter.heroku.com/), suporte a diversas tecnologias como [Ruby](http://www.ruby-lang.org/) ([Ruby on
Rails](http://rubyonrails.org/) ou [Sinatra](http://www.sinatrarb.com/)), [Node.js](http://nodejs.org/), [Clojure](http://clojure.org/), [Java](http://www.java.com/),
[Python](http://www.python.org/), e [Scala](http://www.scala-lang.org/).

Porém, uma das dúvidas de muitos desenvolvedores é quando a aplicação já
está no ambiente heroku em producão em endereço padrão heroku como
*http://minhaaplicacao.herokuapp.com*, o cliente registrou o domínio
*http://minhaaplicacao.com.br* e agora deseja apontar tudo para o lugar
certo.

Como dito, a documentação do heroku é muito boa, e ele fornece [um
tutorial explicando como deve ser registrado o domínio do seu
gerenciador de DNS](https://devcenter.heroku.com/articles/custom-domains), mas o seu problema não é o heroku e sim o
gerenciador de DNS do cliente, que no caso de um registro *.com.br*, é
feito no [registro.br](http://registro.br/) e pode se mostrar bem confuso no começo.

Geralmente são dois tipos de registro de DNS que um cliente pode pedir,
ou apontar um dominio inteiro para sua aplicação, no nosso exemplo
*minhaaplicacao.com.br*, ou um subdomínio, que seria
*subdominio.minhaaplicacao.com.br*. Vou explicar cada um dos casos a
seguir.

## Registro do domínio

Essa configuração é bem simples e consiste em apontar as chamadas
“**minhaaplicacao**.com.br” e “www.**minhaaplicacao**.com.br” para o
heroku, deixando o servidor de DNS configurado no registro.br e
permitindo que sejam cadastradas outras configurações futuramente, como
um subdominio que aponta para outra aplicação, cadastro de DNS do
serviço de email, entre outros.

Para efetuar essa configuração, vá ao painel do registro.br, selecione o
registro (domínio) que deseja efetuar a configuração, na opção *“DNS”*
deixe selecionada a opção *“Utilizar os servidores DNS do Registro.br”*
e em seguida clique em *“Salvar e Editar DNS”*

![heroku](/pixyll/images/2012-04-26-registro-br-e-heroku-configurando-dns/registrobr-dns-menu.png)

Na tela seguinte adicione 6 registros novos (clicando na opção *“+
Record”*) e preencha o tipo como ***“A”*** para todos eles e coloque um
endereço de IP do heroku abaixo na coluna “dados” para cada um dos
registros, sendo que cada um dos IPs deve-se ter um valor com nome vazio
e outro com o nome *“www”*, conforme a imagem abaixo

{% highlight bash %}
75.101.163.44
75.101.145.87
174.129.212.2
{% endhighlight %}

![heroku](/pixyll/images/2012-04-26-registro-br-e-heroku-configurando-dns/registrobr-zonas.png)

## Registro de Subdomínio

Um subdomínio é apenas um apelido para um outro endereço onde o seu
servidor de DNS informa qual o endereço novo que aquela requisição deve
seguir, e o procedimento de resgistro é bastante similar à configuração
de domínio.

Vá ao painel do registro.br, selecione o registro que deseja efetuar a
configuração, na opção *“DNS”* deixe selecionada a opção *“Utilizar os
servidores DNS do Registro.br”* e em seguida clique em *“Salvar e Editar
DNS”*

![heroku](/pixyll/images/2012-04-26-registro-br-e-heroku-configurando-dns/registrobr-dns-menu.png)

Na tela seguinte adicione um registro clicando em *“+Record”*, prencha o seu subdominio no primeiro campo, mude o tipo para `CNAME` e no campo dados preencha com o endereço do seu aplicativo, e atenção: o endereço é sem `http://` ou `https://`

![heroku](/pixyll/images/2012-04-26-registro-br-e-heroku-configurando-dns/registrobr-editar-zona.png)

Em seguida repita esse processo para cada subdomínio novo que deseja cadastrar.

## Configurando o Heroku

A configuração no heroku é extremamente simples, e necessária para que os servidores do heroku saibam que a sua aplicação deve responder a um domínio ou outro.

Para fazer essa configuração, vá para os detalhes da sua aplicação no painel do heroku e adicione o seu dominio na lista de domains

![heroku](/pixyll/images/2012-04-26-registro-br-e-heroku-configurando-dns/heroku-add-domain.png)

Você pode adicionar um * antes do domínio para que a sua aplicação do heroku responda a qualquer chamada, independente do subdomínio, ou adicionar cada um especificamente, como:

{% highlight bash %}
minhaaplicacao.com.br
www.minhaaplicacao.com.br
subdominio.minhaaplicacao.com.br
{% endhighlight %}

Outra maneira de cadastrar os domínios é usando o console, digitando o comando abaixo para cada domínio que deseja adicionar

{% highlight bash %}
$ heroku domains:add www.minhaaplicacao.com.br
{% endhighlight %}

Um ponto que vale chamar a atenção é que essa configuração do heroku é completamente independente de onde você registrou o domínio, seja no registro.br, godaddy.com ou qualquer outro, tudo que o heroku vai fazer é tratar as requisições para o seu domínio nos servidores deles e encaminhá-las para sua aplicação corretamente.

---

Originally posted by me at [http://i.ndigo.com.br/2012/04/registro-br-e-heroku-configurando-dns](https://web.archive.org/web/20130906055035/http://i.ndigo.com.br/2012/04/registro-br-e-heroku-configurando-dns)
