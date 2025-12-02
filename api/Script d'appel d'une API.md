---
title: Script d'appel d'une API
authors: Éric Quinton
license: CC-BY
tags:
  - api
created: 19/08/2025
---
~~~php
<?php

/**
 * Script to send an API request to Collec-Science server
 * 
 * To use it:
 * fill in the variables method, address, page, login, token and params
 * 
 * execute the script in a terminal, with the command:
 * php api.php
 */

/**
 * generic variables
 */
$method = "GET"; // or POST
$address = "https://localhost"; // address of the server
$login = "apilogin"; // login used to send api request
$token = "xxx" ; // Token associated with the login
$page = "apiv1sampleList"; // API to request
/**
 * List of usable pages:
 * apiv1sampleList (GET)
 * apiv1sampleUids (GET)
 * apiv1sampleDisplay (GET)
 * apiv1sampleDelete (POST)
 * apiv1movementWrite (POST)
 * apiv1documents (GET)
 * apiv1documentGet (GET)
 * apiv1documentWrite (POST)
 */

$fileToSend = ""; // location of the file to send (apiv1documentWrite)
/**
 * List of variables to send to the server.
 * Except if a collection is public, only 2 variables are mandatory: login and token,
 * to identify the sender
 */
$params = [
    "login" =>$login,
    "token"=> $token,
    /* "uid" => 1234,
    collection_id = 1,
    ...
    */
];
$debugMode = false; // set to true to see the exchange between curl and the server

/**
 * Functions used by the script
 */
function is_cli(): bool
{
    if (in_array(PHP_SAPI, ['cli', 'phpdbg'], true)) {
        return true;
    }
    return ! isset($_SERVER['REMOTE_ADDR']) && ! isset($_SERVER['REQUEST_METHOD']);
}
/**
 * Method printA
 * 
 * Display the content of a variable (array or not)
 *
 * @param any $arr variable to display
 * @param int $level deepth of interrogation
 * @param array $exclude list of keys to not display (if array)
 *
 * @return void
 */
function printA($arr, $level = 0, $exclude = array())
{
    $childLevel = $level + 1;
    $nl = getLineFeed();

    if (is_array($arr)) {
        foreach ($arr as $key => $var) {
            if (!in_array($key, $exclude)) {
                if (is_object($var)) {
                    $var = (array) $var;
                    $key .= " (object)";
                }
                for ($i = 0; $i < $level * 4; $i++) {
                    echo "&nbsp;";
                }
                echo $key . ": ";
                if (is_array($var)) {
                    echo $nl;
                    printA($var, $childLevel, $exclude);
                } else {
                    print_r($var);
                    echo $nl;
                }
            }
        }
    } else {
        echo "$arr" . $nl;
    }
}

/**
 * Method getLineFeed
 * 
 * get the end of the line according to context
 *
 * @return void
 */
function getLineFeed()
{
    if (is_cli()) {
        return PHP_EOL;
    } else {
        return "<br>";
    }
}

class ApiCurlException extends Exception {};
/**
 * Method makeCurlFile used to send a file (apiv1documentWrite)
 *
 * @param string $file: path of the file to send
 *
 * @return void
 */
function makeCurlFile($file)
{
    $mime = mime_content_type($file);
    $info = pathinfo($file);
    $name = $info['basename'];
    $output = new CURLFile($file, $mime, $name);
    return $output;
}
/**
 * call an api with curl
 * code from
 * @param string $method
 * @param string $url
 * @param array $data
 */
function apiCall($method, $url, $certificate_path = "", $data = array(), $modeDebug = false, $file = "")
{
    $curl = curl_init($url);
    if (!$curl) {
        throw new ApiCurlException(_("Impossible d'initialiser le composant curl"));
    }
    if (!empty($file)) {
        $data["file"] = makeCurlFile($file);
    }
    switch ($method) {
        case "POST":
            curl_setopt($curl, CURLOPT_POST, true);
            if (!empty($data)) {
                curl_setopt($curl, CURLOPT_POSTFIELDS, $data);
            }
            break;
        case "PUT":
            curl_setopt($curl, CURLOPT_CUSTOMREQUEST, "PUT");
            if (!empty($data)) {
                curl_setopt($curl, CURLOPT_POSTFIELDS, $data);
            }
            break;
        default:
            if (!empty($data)) {
                $url = sprintf("%s?%s", $url, http_build_query($data));
                echo "URL: $url" . PHP_EOL;
            }
    }
    /**
     * Set options
     */
    curl_setopt($curl, CURLOPT_URL, $url);
    curl_setopt($curl, CURLOPT_RETURNTRANSFER, 1);
    if (!empty($certificate_path)) {
        curl_setopt($curl, CURLOPT_SSLCERT, $certificate_path);
    }

    curl_setopt($curl, CURLOPT_SSL_VERIFYSTATUS, false);
    curl_setopt($curl, CURLOPT_SSL_VERIFYPEER, false);
    curl_setopt($curl, CURLOPT_SSL_VERIFYHOST, 0);
    if ($modeDebug) {
        curl_setopt($curl, CURLOPT_VERBOSE, true);
    }
    /**
     * Execute request
     */
    $res = curl_exec($curl);
    if ($res === false) {
        throw new ApiCurlException(
            sprintf(
                "Une erreur est survenue lors de l'exécution de la requête vers le serveur distant. Code d'erreur CURL : %s",
                curl_error($curl)
            )
        );
    }
    curl_close($curl);
    return $res;
}

/**
 * Execution of the api call
 */
echo "Méthode : " . $method . PHP_EOL;
echo "Adresse : " . $address . "/" . $page . PHP_EOL;
echo "Paramètres :" . PHP_EOL;
printA($params);
$res = apiCall($method, $address . "/" . $page, "", $params, $debugMode, $fileToSend);
if ($res == "null") {
    echo "résultat : null" . PHP_EOL;
} else {
    if ($page == "apiv1documentGet") {
        file_put_contents("test.txt", $res);
    } else {
        printA(json_decode($res, true));
    }
}

~~~