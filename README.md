Desafio - Processo seletivo
---------------------------------------------------------------
Tarefa # 3 - Apenas frontend
Vamos bagunçar todo o checkout. Você precisa:
1. Tornar o checkout útil para uma transação nacional (brasileira);
2. Remover 2 campos aleatórios da etapa de Frete;
3. Todos os outros nomes de campo, que devem ser escritos ao contrário, como Nome, devem
ser emoN.
4. E o botão da próxima etapa deve redirecionar de volta para o carrinho.
Documente todas as suas alterações para a etapa 2. Assim, saberemos o que foi removido.
Você pode usar qualquer instalação do Magento 2 que tiver.
Anexe também o processo de instalação documentado e o usuário com explicações gerais.
Portanto, teremos certeza de que entendeu-os corretamente.


<h2>Via Composer</h2>
<p>Para essa instalação é necessário ter instalado o <a href="https://getcomposer.org" rel="nofollow">Composer</a> você precisa usar o terminal do seu servidor.</p>

<h2>1º Passo - Baixar o Magento</h2>

Comando usado:
<pre>
<code>composer create-project --repository=https://repo.magento.com/ magento/project-community-edition:2.3.5 m235</code></pre>

<h2>2º Passo - Solucionar dois problemas <p>(pois um deles afeta na instalação).</p></h2>

<p>ERRO: Unable to apply data patch Magento\Theme\Setup\Patch\Data\RegisterThemes for module Magento_Theme. Original exception message: Wrong file</p>

<p>Solução:
https://github.com/magento/magento2/issues/28055</p>

<h3>Problema de barras '/' no Windows</h3>

<p>Problem: 1 exception(s):
Exception #0 (Magento\Framework\Exception\ValidatorException): Invalid template file: 'C:/xampp/htdocs/Hibrido/m235/vendor/magento/module-theme/view/frontend/templates/page/js/require_js.phtml' in module: '' block's name: 'require.js'
</p>
<p>Solução:
https://github.com/magento/magento2/issues/19480</p>


<h2>3º Passo - Instalação | Método Rápido [RECOMENDADO]</h2>

Comando utilizado:
<pre>
$ <code>bin/magento setup:install --backend-frontname=admin --db-name=m235 --db-user=root --db-password="" --db-host=127.0.0.1 --admin-user=admin --admin-password=123123q --admin-email="eu@gustavoferri.com.br" --admin-firstname=Gustavo --admin-lastname=Ferri --currency=BRL --session-save=files </code>
</pre>

<b>Após finalizar a instalação, usar os comandos abaixo:</b>

<pre>
<code>
php bin/magento indexer:reindex
php bin/magento setup:upgrade
php bin/magento setup:static-content:deploy -f
php bin/magento cache:flush
</code>
</pre>


<h2>4º Passo - Instalação do Sample Data </h2>

<p>Comandos:</p>

<pre>
<code>
php bin/magento sampledata:deploy
php bin/magento module:enable --all
php bin/magento setup:upgrade
php bin/magento cache:flush
php bin/magento cache:clean
</code>
</pre>
----
<p>Fonte: https://mirasvit.com/knowledge-base/magento-2-installation-guide-composer-sample-data.html</p>

<h2>5º Passo - Setando Modo desenvolvedor</h2>

<pre>
<code>
$ bin/magento deploy:mode:set developer
Enabled developer mode.
</code>
</pre>

<h2>6º Passo - Traduzindo o Magento para PT-BR </h2>

<pre><code>composer require rafaelstz/traducao_magento2_pt_br:dev-master
php bin/magento setup:static-content:deploy pt_BR -f
php bin/magento cache:clean
</code></pre>

<h2> ou manualmente </h2>
<ul>
<li>Crie o diretório <strong>app/i18n/rafaelcg/language_pt_br</strong></li>
<li>Efetue o <a href="https://github.com/rafaelstz/traducao_magento2_pt_br/archive/master.zip">download do zip</a></li>
<li>Mova o conteúdo do repositório para a pasta e habilite a tradução</li>
</ul>

<h2>7º Passo - Instalação do Módulo BrazilCustomerAttributes <p>(Para adaptar os campos de clientes e endereços para o Brasil).</p></h2>
<p>https://github.com/m2-systemcode/BrazilCustomerAttributes</p>

<pre><code>composer require systemcode/brazilcustomerattributes
php bin/magento module:enable SystemCode_BrazilCustomerAttributes SystemCode_Base
php bin/magento setup:upgrade </code></pre>

-----------------------------------------------
<h2>Subindo magento no Github</h2>
-----------------------------------------------
<pre>
$<code>git add .
$ git commit -m "Adicionado Magento 2.3.5"
$ git remote add origin https://github.com/gustavoferri/desafio-hibrido.git
$ git push -u origin master </code></pre>
----------------

<h3>Remover 2 campos aleatórios da etapa de Frete;<h3>

<p>Foram removidos o campo Bairro e Número
Segue print:
<img src="https://www.gustavoferri.com.br/hibrido/print-remover-campos.png">

<h3>3. Todos os outros nomes de campo, que devem ser escritos ao contrário, como Nome, devem
ser emoN.</h3>

<p> Foram alterados todos os nomes dos campos do Checkout via .csv
<p>Arquivo:<strong>app/i18n/rafaelcg/language_pt_br/pt_BR.csv</strong></p>

<h4>4. E o botão da próxima etapa deve redirecionar de volta para o carrinho.
Documente todas as suas alterações para a etapa 2. Assim, saberemos o que foi removido.
Você pode usar qualquer instalação do Magento 2 que tiver.
Anexe também o processo de instalação documentado e o usuário com explicações gerais.
Portanto, teremos certeza de que entendeu-os corretamente.</h4>

arquivo:
<code>\vendor\magento\module-checkout\view\frontend\web\template\shipping.html</code>
</code><a href="https://github.com/gustavoferri/desafio-hibrido/blob/master/app/design/frontend/Magento/luma/Magento_Checkout/web/template/shipping.html">\app\design\frontend\Magento\luma\Magento_Checkout\web\template</code>
<p> Adicionado  </p>

<code><!-- BUTTON -->
Botão - Voltar p/ Carrinho
</code>

<h4>Segue print da página:</h4>
<img src="https://www.gustavoferri.com.br/hibrido/print-checkout-m2.png">


