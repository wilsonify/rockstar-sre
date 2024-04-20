FROM node:16 as builder
WORKDIR /usr/src/app
COPY . /usr/src/app
RUN npm install
RUN ldd /usr/local/bin/node

FROM scratch
WORKDIR /usr/src/app

COPY --from=builder "/lib/x86_64-linux-gnu/libc.so.6" "/lib/x86_64-linux-gnu/libc.so.6"
COPY --from=builder "/lib/x86_64-linux-gnu/libdl.so.2" "/lib/x86_64-linux-gnu/libdl.so.2"
COPY --from=builder "/lib/x86_64-linux-gnu/libgcc_s.so.1" "/lib/x86_64-linux-gnu/libgcc_s.so.1"
COPY --from=builder "/lib/x86_64-linux-gnu/libm.so.6" "/lib/x86_64-linux-gnu/libm.so.6"
COPY --from=builder "/lib/x86_64-linux-gnu/libpthread.so.0" "/lib/x86_64-linux-gnu/libpthread.so.0"
COPY --from=builder "/lib64/ld-linux-x86-64.so.2" "/lib64/ld-linux-x86-64.so.2"
COPY --from=builder "usr/lib/x86_64-linux-gnu/libstdc++.so.6" "/usr/lib/x86_64-linux-gnu/libstdc++.so.6"
COPY --from=builder "/usr/local/bin/node" "/usr/local/bin/node"
COPY --from=builder "/usr/src/app/node_modules" "/usr/src/app/node_modules"
COPY --from=builder "/usr/src/app/server.js" "/usr/src/app/server.js"
EXPOSE 8080
CMD [ "node", "server.js" ]










