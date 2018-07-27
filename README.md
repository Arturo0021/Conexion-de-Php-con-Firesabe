# Conexion-de-Php-con-Firesabe
Este Archivo se Conecta con Firebase para hacer peticiones y mandar las push notification

<?php
header('Content-type: application/json');
$token = $_GET['tok'];

    #API access key from Google API's Console
    define( 'API_ACCESS_KEY', ' --------------------- ' );
    #prep the bundle
     $msg = array
          (
		'body' 	=> 'Cuerpo Mensaje',
		'title'	=> 'Título mensaje',
        'icon'	=> 'myicon',
        'sound' => 'mySound',
        'Extras' => 'Parametros extras'
          );

	$fields = array
			(
				'from'          => 'TIII',
				'to'		    => $token,
				'notification'	=> $msg,
				'data'          => $msg
			);
	
	
	$headers = array
			(
				'Authorization: key=' . API_ACCESS_KEY,
				'Content-Type: application/json'
			);

#Send Reponse To FireBase Server	
		$ch = curl_init();
		curl_setopt( $ch,CURLOPT_URL, 'https://fcm.googleapis.com/fcm/send' );
		curl_setopt( $ch,CURLOPT_POST, true );
		curl_setopt( $ch,CURLOPT_HTTPHEADER, $headers );
		curl_setopt( $ch,CURLOPT_RETURNTRANSFER, true );
		curl_setopt( $ch,CURLOPT_SSL_VERIFYPEER, false );
		curl_setopt( $ch,CURLOPT_POSTFIELDS, json_encode($fields) );
		$result = curl_exec($ch);
		curl_close( $ch );
    
    $res_row = json_decode($result, true);
    array_push($array_result, $res_row);
#Echo Result Of FireBase Server
echo json_encode($array_result);
?>
