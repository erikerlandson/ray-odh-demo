FROM docker.io/rayproject/ray:nightly

# ray dumps stuff into /root/conda as ROOT
# because of course it does
#RUN chmod -R go+rwx /root

COPY run-with-server /opt/ray/bin/
