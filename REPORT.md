# Relatório 3ª Entrega

---

O desenvolvimento da solução para a 3ª entrega utilizou o algoritmo gossip modificado. É também de notar que foram utilizados os ficheiros .proto no Contract disponibilizados.

Relativamente aos pedidos de update cada cliente envia um pedido com a sua operação e o seu timestamp. Após a receção do
pedido por parte do servidor este verifica se o realizou comparando o seu replica timestamp com o timestamp do
pedido, de modo a não adicionar operações duplicadas (função checkOperationRegistrable). Como tal, tornou-se desnecessário
o uso de uma executed operation table. Sendo a operação não repetida, esta é colocada tanto no distLedger como nas operações
não propagadas do server. A entrada correspondente ao servidor do replica timestamp é incrementada em uma unidade
e esse valor é colocado na entrada do timestamp adicionado à operação e devolvido ao cliente (que efetua merge do timestamp).
Relativamente à estabilidade de um update, este só é efetuado quando o value timestamp do servidor em questão é superior ao previous
timestamp da operação na lista de operações instáveis.

Aquando de um recebimento de um pedido gossip o servidor recipiente adiciona ao seu unstable operation log cada 
operação recebida, tendo cuidado para não adicionar operações que já constem deste log ou do seu executed operation log e mantendo a causal
order. De seguida faz merge do replica timestamp recebido com o seu replica timestamp e procede a sucessivas tentativas de execução das operações 
no seu unstable operation log até o percorrer todo, terminando o gossip. Deste modo, são também tido em conta operações que possam ter ficado
executable como consequência do gossip. Foi também tida a precaução de realizar lookup antes dos pedidos de gossip
em que ainda não foram criados stubs para outros servidores, de modo a poder detetar o registo de um servidor que ainda não foi refletido no value timestamp do servidor e stubs.

Por fim, relativamente aos pedidos de leitura, estes são mantidos em espera até se verificar que o value timestamp do servidor do pedido é maior ou igual
ao previous timestamp do pedido. Para notificar a espera é efetuado um notify na função que altera o timestamp e pode tornar a condição
que permite a execução do pedido verdadeira. Aquando da realização da query é devolvido ao cliente o value timestamp do servidor e este efetua
merge com o seu timestamp.








