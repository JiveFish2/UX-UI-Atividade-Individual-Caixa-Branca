# UX-UI-Atividade-Individual-Caixa-Branca
Repositório da primeira parte da atividade individual caixa branca 

Codigo fornecido para a atividade

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

Definição dos Nós 
Nó 1:

String sql = "";

Connection conn = conectarBD();

Construção da string sql

Nó 2 (Bloco Try):

Statement st = conn.createStatement();

ResultSet rs = st.executeQuery(sql);

Nó 3 (Decisão P1):

if (rs.next())

Nó 4 (Bloco If-True):

nome = rs.getString("nome");

return true;

Nó 5 (Bloco Catch):

catch (Exception e) { }

Nó 6 (Return Final):

return result;

Nó 7 (Fim):

Ponto de saída do método.

Definição das Arestas 

1 -> 2: Fluxo padrão do início para o bloco try.

2 -> 3: O try foi bem-sucedido e o fluxo segue para a decisão if.

2 -> 5: O try falhou (gerou uma exceção) e o fluxo desvia para o catch.

3 -> 4: A condição if foi verdadeira.

3 -> 6: A condição if foi falsa.

4 -> 7: O método termina após o return true.

5 -> 6: O bloco catch termina e o fluxo segue para o return final.

6 -> 7: O método termina após o return result.
