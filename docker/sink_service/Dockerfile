FROM wirepas/gateway_base_builder:edge AS builder

WORKDIR /home/wirepas

COPY --chown=wirepas ./sink_service /home/wirepas/sink_service

WORKDIR /home/wirepas/sink_service

RUN make

FROM ubuntu:20.04

RUN useradd -ms /bin/bash wirepas
RUN usermod -a -G dialout wirepas

# Copy the built service and its dependencies from builder
COPY --from=builder /home/wirepas/sink_service/build/sinkService /home/wirepas/

USER wirepas

CMD ["stdbuf", "-oL", "-eL", "/home/wirepas/sinkService"]
