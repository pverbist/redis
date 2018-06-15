# Copyright 2016 The Kubernetes Authors.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

FROM centos

RUN yum -y install epel-release 
RUN yum -y install hostname http://rpms.famillecollet.com/enterprise/7/remi/x86_64//redis-4.0.10-1.el7.remi.x86_64.rpm; yum clean all ; rm -rf /var/cache/yum

ADD https://storage.googleapis.com/kubernetes-release/release/v1.6.4/bin/linux/amd64/kubectl /usr/local/bin/kubectl
RUN chmod +x /usr/local/bin/kubectl

COPY label-updater.sh /usr/local/bin/label-updater.sh
COPY redis-launcher.sh /usr/local/bin/redis-launcher.sh
COPY promote.sh /usr/local/bin/promote.sh

COPY redis-master.conf /redis-master/redis.conf
COPY redis-slave.conf /redis-slave/redis.conf
COPY runner.txt /redis-runner/runner.txt
RUN mkdir -p /redis-sentinel ; chmod -R 777 /redis-sentinel /redis-slave /redis-runner

CMD [ "chmod +x /usr/local/bin/redis-launcher.sh" ]
CMD [ "/usr/local/bin/redis-launcher.sh | tee /redis-runner/runner.txt" ]

ENTRYPOINT [ "bash", "-c" ]
