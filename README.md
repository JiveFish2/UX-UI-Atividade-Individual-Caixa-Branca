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
