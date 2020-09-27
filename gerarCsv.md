<?php
/**
 * Relatorio p;
 *
 * @package Relatorio
 * @author Guilherme Pires
 *
 * @return (file) um arquivo em pdf no formato desejado;
 */

$fileName = "ProdutoTabelaCusto" . "_" . date_format(new DateTime("Now"), 'd-m-Y') . ".csv";

header('Content-Type: text/html; charset=utf-8');
header ('Content-type: text' );
header('Content-disposition: ' . (strpos("teste", "txt")?"inline":"attachment") .'; filename="' . $fileName . '"');    


/**
 * @define (string) DS - Directory separator.
 */
define("DS", "/", true);

$base_path = "";
for ($i = 2; $i < (int) substr_count($_SERVER['PHP_SELF'], DS); $i++) {
	$base_path .= '../';
}

/**
 * @define (string) BASE_PATH_OPEN - Best Root Path.
 */
define("BASE_PATH_OPEN", $base_path, true);

/** Files needed for the application **/
include_once BASE_PATH_OPEN . 'util.class.php';
include_once BASE_PATH_OPEN . 'config_sessao.php';

include_once BASE_PATH_OPEN . 'dao' . DS . 'conexao.php';


$con = new Conexao();

/***************************************************************************************************************
Variaveis  - passadas p/ o calculo;
/**************************************************************************************************************/

$idempresa = $_SESSION['pegaVariabeis'];


// Verificador de seleção da tabela;

$con = $con->getConexao(); // Obtendo a Conexao com a base;

/****************************************************************************************************************
- -   IMPRIMINDO CSV   - -
/***************************************************************************************************************/

$query = "
    SELECT  * from ...";
$stmt = $con->query($query);
$resultado = $stmt->fetchAll();


//IMPRESSAO DO CABEÇALHO DOS ITENS

echo utf8_decode("Relatório de Tabela de Preço")."\n";
echo "\n".utf8_decode("por Cliente");
echo "\n". utf8_decode("Referência: " . $resultado["descricao"]);
echo "\n".utf8_decode("Data de Emissão: " . date_format(new DateTime("Now"), 'd/m/Y  à\s  H\hi'))."\n";

echo "\n;".$arrayTamCol['1'], 5, utf8_decode("- CODIGO -").";".
$arrayTamCol['2'], 5, utf8_decode("- PRODUTO -").";".
$arrayTamCol['3'], 5, utf8_decode("- MARCA -").";".
$arrayTamCol['4'], 5, utf8_decode("- VALOR -")."\n";
foreach ($resultado as $dadosPedido) {

   
    $texto = ";".utf8_decode(str_pad($dadosPedido['..'], 15, ' ', STR_PAD_LEFT)).";".
    utf8_decode($dadosPedido['..']).";".
    utf8_decode("  " . str_pad($dadosPedido['..'], 52, ' ', STR_PAD_BOTH)).";".
    utf8_decode(str_pad(Util::mostraValor($novo_valor, 2), 28, ' ', STR_PAD_LEFT))."\n";
    
    echo $texto;

	$somaTotal += $novo_valor;

}

/***************************************************************************************************************
IMPRIMINDO  - As linhas finais;
/**************************************************************************************************************/
	$texto =";".utf8_decode(str_pad(" -*- ", 14, ' ', STR_PAD_LEFT)).";".
			utf8_decode(str_pad(" -*-", 58, ' ', STR_PAD_LEFT)).";".
			utf8_decode(str_pad(" -*- ", 36, ' ', STR_PAD_LEFT)).";".
			utf8_decode(str_pad(" -*- ", 26, ' ', STR_PAD_LEFT));
    echo $texto;
?>
