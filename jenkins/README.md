# jenkins

Dockerhubとリンクしています。

https://hub.docker.com/repository/docker/shiftrepo/docker-jenkins

docker-composeで起動する。

### パスワード表示
docker exec -it jenkins_jenkins_1 cat /var/jenkins_home/secrets/initialAdminPassword

http://localhost:8080/scriptに以下のgroovyスクリプトを入力して実行すると取得できます。

~~~groovy
Jenkins.instance.pluginManager.plugins.each{
 plugin -> println("${plugin.getShortName()}")
 
}
~~~


参考
https://qiita.com/uni-3/items/62f072954edb67a1e58d

呪文
docker-compose down --rmi all --volumes
