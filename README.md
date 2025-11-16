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

Codigo alterado

    package login;

    import java.sql.Connection;
    import java.sql.DriverManager;
    import java.sql.ResultSet;
    import java.sql.Statement;

    public class Autenticador {

    // Variável de instância para o nome
    public String nomeDoUsuario = "";

    // Tenta estabelecer uma conexão com o banco, retorna null se falhar
     
    public Connection getConexao() {
        Connection conexao = null;
        String url = "jdbc:mysql://127.0.0.1/test?user=Lopes&password=123";
        try {
            // tentativa de conexão
            Class.forName("com.mysql.Driver.Manager").newInstance();
            conexao = DriverManager.getConnection(url);

        } catch (Exception e) {
        }
        
        // Ponto de retorno 
        return conexao;
    }

    // Verifica as credenciais do usuário
    
    public boolean checarLogin(String login, String senha) {
        
        boolean acessoPermitido = false; 
        String querySQL = "SELECT nome FROM usuarios " +
                          "WHERE login = '" + login + "' " +
                          "AND senha = '" + senha + "';";

        Connection conn = this.getConexao();
        Statement comando = null;
        ResultSet resultado = null;
        try { 
            comando = conn.createStatement();
            resultado = comando.executeQuery(querySQL);

            // Bloco de decisão
            if (resultado.next()) {
                // Caminho de sucesso
                this.nomeDoUsuario = resultado.getString("nome");
                acessoPermitido = true;
            }
            
            // (else vai para finally e return
        } catch (Exception e) {
        }
        return acessoPermitido;
    }    
    }

2. Complexidade Ciclomática (V(G))
O cálculo (V(G)) nos diz quantos testes são necessários para cobrir todas as lógicas.

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

3. Caminhos Básicos
Com V(G) = 3, precisamos destes 3 casos de teste:

Caminho 1: Sucesso (Usuário Encontrado)

Percurso: 1 → 2 → 3(true) → 4 → 6 → 7

Teste: Login e senha corretos.

Caminho 2: Falha (Usuário Não Encontrado)

Percurso: 1 → 2 → 3(false) → 6 → 7

Teste: Login ou senha incorretos.

Caminho 3: Exceção (Erro no Banco)

Percurso: 1 → 2 → 5 → 6 → 7

Teste: Simular uma falha de conexão (ex: conn nulo ou banco offline).
