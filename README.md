# UX-UI-Atividade-Individual-Caixa-Branca
Repositório da primeira parte da atividade individual caixa branca 

Código fornecido para a atividade

    package login;

    import java.sql.Connection;
    import java.sql.DriverManager;
    import java.sql.ResultSet;
    import java.sql.Statement;

    public class User   {
    public Connection conectarBD() {
    Connection conn = null;
    try{
        Class.forName("com.mysql.Driver.Manager").newInstance();
        String url = "jdbc:mysql://127.0.0.1/test?user=Lopes&password=123";
        conn = DriverManager.getConnection(url);
    } catch (Exception e) { }
    return conn; }
    
    public String nome = "";
    public boolean result = false;
    public boolean verificarUsuario(String login, String senha) {
    String sql = "";
    Connection conn = conectarBD();
    //Intrução SQL 
    sql += "select nome from usuarios ";
    sql +="where login = " + "'" + login + "'";
    sql += " and senha = " + "'" + senha + "';";
    try {
        Statement st = conn.createStatement();
        ResultSet rs = st.executeQuery(sql);
        if (rs.next()) {
            return true;
            nome = rs.getString("nome");
        }catch (Exception e) {  }
    return result; }
    }//fim da class

Fluxo de Controle

Grafo de Fluxo

Nó 1: Início (Declaração de sql, chamada conectarBD(), construção da string SQL)

Nó 2: Bloco try (Criação do Statement, execução do executeQuery)

Nó 3: Decisão if (rs.next())

Nó 4: Bloco if-true (return true; e nome = ... (inalcançável))

Nó 5: Bloco catch (Captura da exceção)

Nó 6: Fim do try-catch e return result;

Nó 7: Fim do método

Arestas (Fluxo de Controle):

1 → 2 (Fluxo normal)

2 → 3 (Sucesso no try, vai para o if)

2 → 5 (Erro no try, pula para o catch)

3 → 4 (if é verdadeiro)

3 → 6 (if é falso)

4 → 7 (Sai do método)

5 → 6 (Sai do catch e continua)

6 → 7 (Sai do método)

Complexidade Ciclomática

Resultado: V(G) = 3

Cálculo (Nós e Arestas):

Nós (N) = 7

Arestas (A) = 8

V(G) = Arestas – Nós + 2

V(G) = 8 – 7 + 2

V(G) = 3

Cálculo (Pontos de Decisão):

Decisões (P) = 2 (1. o try-catch, 2. o if)

V(G) = Decisões + 1

V(G) = 2 + 1

V(G) = 3

Caminhos Básicos
Com base no V(G) = 3, estes são os 3 caminhos de teste necessários:

Caminho 1: Sucesso (Usuário Encontrado)

Percurso: 1 → 2 → 3(true) → 4 → 7

Teste: Login e senha corretos.

Caminho 2: Falha (Usuário Não Encontrado)

Percurso: 1 → 2 → 3(false) → 6 → 7

Teste: Login ou senha incorretos.

Caminho 3: Exceção (Erro no Banco)

Percurso: 1 → 2 → 5 → 6 → 7

Teste: Simular uma falha de conexão (ex: conn nulo ou banco offline).
