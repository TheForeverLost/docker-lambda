FROM lambci/lambda-base-2:build

ENV PATH=/var/lang/bin:$PATH \
    LD_LIBRARY_PATH=/var/lang/lib:$LD_LIBRARY_PATH \
    AWS_EXECUTION_ENV=AWS_Lambda_java11

RUN rm -rf /var/runtime /var/lang /var/rapid && \
  curl https://lambci.s3.amazonaws.com/fs/java11.tgz | tar -zx -C / && \
  mkdir /usr/local/gradle && curl -L -o gradle.zip https://downloads.gradle-dn.com/distributions/gradle-6.2.2-bin.zip && \
  unzip -d /usr/local/gradle gradle.zip && rm gradle.zip && mkdir /usr/local/maven && \
  curl -L http://mirror.cc.columbia.edu/pub/software/apache/maven/maven-3/3.6.3/binaries/apache-maven-3.6.3-bin.tar.gz | \
  tar -zx -C /usr/local/maven

ENV PATH="/usr/local/gradle/gradle-6.2.2/bin:/usr/local/maven/apache-maven-3.6.3/bin:${PATH}"

# Add these as a separate layer as they get updated frequently
RUN pip install -U awscli boto3 aws-sam-cli==0.47.0 aws-lambda-builders==0.8.0 --no-cache-dir
