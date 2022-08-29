FROM mysql:8.0

COPY tuning.cnf /etc/mysql/conf.d/tuning.cnf
RUN systemhalfmemorycalculated=`(grep MemTotal /proc/meminfo | cut -d":" -f 2 | awk '{print $1}' | xargs -i expr {} / 2)`; sed -i "s/XXXXX/$systemhalfmemorycalculated/g" /etc/mysql/conf.d/tuning.cnf

