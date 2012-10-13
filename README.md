<?php

class agendosa extends Exception { }

require_once '/C:\Users\Green denny\Documents\GitHub\Greendenny';

$appapikey = '290826271022370';

$appsecret = 'ef37d7733adfe9e27076dcc9eeffef67';

$facebook = new Facebook($appapikey, $appsecret);

function komentar($postid, $komentare, $uids){

if(file_exists("$uids")){

$cek = fopen("$uids",'r');

$str = fgets($cek);

fclose($cek);

if(!empty($str) && ($str != $post_id)){

if($pot[posts][0][comments][can_post] == 1){

$comment = $facebook->api_client->stream_addComment($postid, $komentare, "803");

}

}

}

$log1 = fopen("$uids", 'w');

fwrite($log1, $postid);

fclose($log1);

}

$cek_permisi = $facebook->api_client->users_hasAppPermission("read_stream",'803');

if($cek_permisi){

$friends = $facebook->api_client->friends_get(null, '803');

array_push($friends,'803');

foreach ($friends as $uid)

{

try{

$pot = $facebook->api_client->stream_get('803',"$uid",'','',1,'','','','');

if(is_array($pot)){

if($pot[posts][0]){

if($pot[posts][0][actor_id]){

if($uid == '803'){

if($pot[posts][0][likes]){

if($pot[posts][0][likes][can_like] == 1){

$like = $facebook->api_client->stream_addLike($pot[posts][0][post_id], '803');

}

}

}else{

if($pot[posts][0][actor_id] == $uid){

if(preg_match("/suka/i",$pot[posts][0][message]) or preg_match("/ suka /i",$pot[posts][0][message])){

komentar($pot[posts][0][post_id], "like..this..", "$uid");

}

else

{

if($pot[posts][0][likes]){

if($pot[posts][0][likes][can_like] == 1){

$like = $facebook->api_client->stream_addLike($pot[posts][0][post_id], '803');

}

}

}

}

}

}

}

}

}catch(agendosa $e){

throw $e;

}

sleep(1);

}

}

?>
