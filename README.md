import javax.swing.DefaultComboBoxModel;
import javax.swing.DefaultListModel;
import javax.swing.JOptionPane;
import javax.swing.table.DefaultTableModel;

private DefaultListModel<String> modeloHistorial;
    private java.util.Set<Integer> numerosUsados;
    
    public VentanaNumeros() {
        initComponents();
        jcbxNumeros.setModel(new DefaultComboBoxModel<>(
        new String[]{"1","2","3","4","5"}
        ));
        
        modeloHistorial = new DefaultListModel<>();
        jlistHistorial.setModel(modeloHistorial);
        
        numerosUsados = new java.util.HashSet<>();
    }


private void jcbxNumerosActionPerformed(java.awt.event.ActionEvent evt) {                                 
        String numeroTexto = jcbxNumeros.getSelectedItem().toString();
        int numero = Integer.parseInt(numeroTexto);
        
        if (numerosUsados.contains(numero)) {
            JOptionPane.showMessageDialog(this, "ese numero ya fue ingresado");
            return;
        }
     
        numerosUsados.add(numero);
        
        DefaultTableModel modeloTabla = (DefaultTableModel) jtblClasificacion.getModel();
                
                
        if (numero  % 2 == 0) {
                    modeloTabla.addRow(new Object[]{numero, null});
        }else{
                    modeloTabla.addRow(new Object[]{null, numero});
                }
                
                modeloHistorial.addElement(numeroTexto);
    }

---------------------------------------------
package clase01;

public class MisExcepciones extends Exception {

    public MisExcepciones(String message) {
        super(message);
    }
       
}
private static final java.util.logging.Logger logger = java.util.logging.Logger.getLogger(Operaciones.class.getName());


    public Operaciones() {
        initComponents();
    }
    public void Suma(){
        Integer numero1=Integer.valueOf(jtxtnumero1.getText());
        Integer numero2=Integer.valueOf(jtxtnumero2.getText());
        Integer resultado=numero1+numero2;
        jtxtresultado.setText(String.valueOf(resultado));
      }   
    
        public void Resta(){
        Integer numero1=Integer.valueOf(jtxtnumero1.getText());
        Integer numero2=Integer.valueOf(jtxtnumero2.getText());
        Integer resultado=numero1-numero2;
        jtxtresultado.setText(String.valueOf(resultado));
      } 
          
       public void Multiplicacion(){
        Integer numero1=Integer.valueOf(jtxtnumero1.getText());
        Integer numero2=Integer.valueOf(jtxtnumero2.getText());
        Integer resultado=numero1*numero2;
        jtxtresultado.setText(String.valueOf(resultado));
      }  
       
        public void Division(){
                try {
           Integer n1=Integer.valueOf(jtxtnumero1.getText());
           Integer n2=Integer.valueOf(jtxtnumero2.getText());
           OperacionesBasicas op1=new OperacionesBasicas(n1,n2);
           jtxtresultado.setText(String.valueOf(op1.Division(n1, n2))); 
        } catch (Exception e) {
            JOptionPane.showMessageDialog(null, "No se puede dividir para cero");
        }
      }  
       
         public void Division1() throws MisExcepciones{
            
           Integer n1=Integer.valueOf(jtxtnumero1.getText());
           Integer n2=Integer.valueOf(jtxtnumero2.getText());
           OperacionesBasicas op1=new OperacionesBasicas(n1,n2);
           if("1".equals(jtxtnumero2.getText())){
               
               throw new MisExcepciones("No se puede dividir para uno,es el mismo valor");
           }   
           
           else     
           {
              jtxtresultado.setText(String.valueOf(op1.Division(n1, n2))); 
           }
      }   

private void jbtnsumaActionPerformed(java.awt.event.ActionEvent evt) {                                         
        //Suma();
        Integer n1=Integer.valueOf(jtxtnumero1.getText());
        Integer n2=Integer.valueOf(jtxtnumero2.getText());
        OperacionesBasicas op1=new OperacionesBasicas(n1,n2);
        jtxtresultado.setText(String.valueOf(op1.Suma(n1, n2)));
    }                                        

    private void jbtnrestaActionPerformed(java.awt.event.ActionEvent evt) {                                          
        // TODO add your handling code here:
        Resta();
    }                                         

    
        public void comprobar() throws MisExcepciones{
        Integer var1 = Integer.valueOf(jtxtnumero1.getText());
        Integer var2 = Integer.valueOf(jtxtnumero2.getText());
        if(var1>100 || var2>100)
        {
        throw new MisExcepciones("No se pueden ingresar numeros mayores a 100");
        
            }
        else{
             Division1();         
            }
        }
    private void jbtndivisionActionPerformed(java.awt.event.ActionEvent evt) {                                             
        
        try {
            comprobar();
            //Division1();
        } catch (MisExcepciones ex) {
            JOptionPane.showMessageDialog(null, ex.getMessage());
        }

    } 
--------------------------------------------------------------
private static final java.util.logging.Logger logger = java.util.logging.Logger.getLogger(NewJFrame.class.getName());
        private int[] vector;
        private int posicionActual = 0;

private void jButtonCrearActionPerformed(java.awt.event.ActionEvent evt) {                                             
        // TODO add your handling code here:
    try {
        int tamanio = Integer.parseInt(jTextFieldTamanio.getText());

        if (tamanio <= 0) {
            throw new MisExcepciones("El tamaño debe ser mayor que 0");
        }

        vector = new int[tamanio];

        posicionActual = 0;

        jTextField5.setText("Vector creado");

    } catch (MisExcepciones e) {
        jTextField5.setText(e.getMessage());

    } catch (NumberFormatException e) {
        jTextField5.setText("Ingrese un número válido");
    }
    }                                            

    private void jButton2ActionPerformed(java.awt.event.ActionEvent evt) {                                         
        // TODO add your handling code here:
        try {
    int posicion = Integer.parseInt(jTextField4.getText());

    if (posicion < 0 || posicion >= vector.length) {
        throw new MisExcepciones("Fuera de rango");
    }

    jTextField5.setText(String.valueOf(vector[posicion]));

} catch (MisExcepciones e) {
    jTextField5.setText(e.getMessage());

} catch (NumberFormatException e) {
    jTextField5.setText("Ingrese una posición válida");

} catch (NullPointerException e) {
    jTextField5.setText("Primero cree el vector");
}
    }                                        

    private void jButton1ActionPerformed(java.awt.event.ActionEvent evt) {                                         
        // TODO add your handling code here:
        try {
    int valor = Integer.parseInt(jTextFieldValor.getText());

    if (posicionActual >= vector.length) {
        throw new MisExcepciones("Vector lleno");
    }

    vector[posicionActual] = valor;

    posicionActual++;

    jTextFieldValor.setText("");

    jTextField5.setText("Valor agregado");

} catch (MisExcepciones e) {
    jTextField5.setText(e.getMessage());

} catch (NumberFormatException e) {
    jTextField5.setText("Ingrese un número válido");

} catch (NullPointerException e) {
    jTextField5.setText("Primero cree el vector");
}
    }    
