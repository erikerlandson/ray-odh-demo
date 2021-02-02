FROM quay.io/erikerlandson/ray:nightly-py36-20210202

# ray dumps stuff into /root/conda as ROOT
# because of course it does
#RUN chmod -R go+rwx /root

COPY run-with-server /opt/ray/bin/
