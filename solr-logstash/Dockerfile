FROM docker.elastic.co/logstash/logstash-oss:6.2.1
# install solr plugin
RUN cd /usr/share/logstash/ && bin/logstash-plugin install logstash-output-solr_http
# https://discuss.elastic.co/t/solr6-logstash-5-timestamp-error/67223
COPY solr_http.rb /usr/share/logstash/vendor/bundle/jruby/2.3.0/gems/logstash-output-solr_http-3.0.4/lib/logstash/outputs/solr_http.rb
# https://discuss.elastic.co/t/logstash-solr-http-plugin-not-working/86217/3
# but seems to work in logstash 6.2 (had problems with 5.4)
#RUN export PATH=/usr/share/logstash/vendor/jruby/bin:$PATH && /usr/share/logstash/vendor/jruby/bin/gem install rsolr -v 1.1.2 && sed -i 's|require "rsolr"|require "/usr/share/logstash/vendor/jruby/lib/ruby/gems/shared/gems/rsolr-1.1.2/lib/rsolr"|' /usr/share/logstash/vendor/bundle/jruby/1.9/gems/logstash-output-solr_http-*/lib/logstash/outputs/solr_http.rb 
ADD config/ /usr/share/logstash/config/
# these volumes need to be set, /data will be scanned regularly
VOLUME /data
# the pipeline configurations need to be there during the start of the container
VOLUME /usr/share/logstash/pipeline/