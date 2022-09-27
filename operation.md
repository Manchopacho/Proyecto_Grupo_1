
package test;
import bean.Producto;
import connection.DBConnection;
import java.sql.ResultSet;


import java.sql.Statement;
import static test.OperacionesBD.actualizarProducto;
        
public class OperacionesBD {

   
    public static void main(String[] args) {
        actualizarProducto("manzana", "bogota");
        listarProducto();
        
    }
    public static void actualizarProducto(String fruta, String ciudad){
    DBConnection con = new DBConnection();
    String sql="UPDATE producto SET ciudad = '" + ciudad + "' WHERE fruta = '" +fruta+ "'";
    try{
        Statement st= con.getConnection().createStatement();
        st.executeUpdate(sql);
        }catch(Exception ex){
        System.out.println(ex.getMessage());
        }
    finally {con.desconectar();}
    }
          
    public static void listarProducto(){
    DBConnection con = new DBConnection();
    String sql="SELECT * FROM producto";
    try{
        Statement st= con.getConnection().createStatement();
        ResultSet rs = st.executeQuery(sql);
        while(rs.next()){
            String fruta = rs.getString("fruta");
            String unidad_de_medida = rs.getString("unidad_de_medida");
            int precio_por_unidad = rs.getInt("precio_por_unidad");
            String ciudad = rs.getString("ciudad");
            String descrpcion = rs.getString("descripcion");
            boolean cantidad = rs.getBoolean("cantidad");
            
            Producto productos = new Producto(fruta, unidad_de_medida, precio_por_unidad, ciudad, descrpcion, cantidad);
            System.out.println(productos.toString());
        }
        }catch(Exception ex){
        System.out.println(ex.getMessage());
        }
    finally {con.desconectar();}
}
}
