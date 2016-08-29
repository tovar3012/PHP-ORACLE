# PHP-ORACLE
Conexion de PHP a Oracle

<?php 
class database{
    private $conexion; 
    
    public function open(){
    	if(!isset( $this->conexion )){
            $this->conexion = oci_connect('user', 'pass', 'base_datos');
            if (!$this->conexion) {
                oci_error();
            }
        }
    }

    public function close(){
    	oci_close($this->conexion);
    }

    public function consulta($sql){
    	$this->open();
    	$r = oci_parse($this->conexion, $sql);
		oci_execute($r);
		return $r;
		oci_free_statement($r);
        $this->close();
    }
}
?>
