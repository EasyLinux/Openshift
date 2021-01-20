FROM alpine:3.12 
LABEL author="Serge NOEL <serge.noel@easylinux.fr>"

# By default, Etherpad container is built and run in "production" mode. This is
# leaner (development dependencies are not installed) and runs faster (among
# other things, assets are minified & compressed).
ENV NODE_ENV=production

# Follow the principle of least privilege: run as unprivileged user.
#
# Running as non-root enables running this image in platforms like OpenShift
# that do not allow images running as root.
RUN apk add nodejs npm \ 
    && adduser -u 5001 -D etherpad \ 
    && mkdir -p /app/etherpad-lite && chown etherpad:0 /app/etherpad-lite

USER etherpad
WORKDIR /app/etherpad-lite
COPY --chown=etherpad:0 ./etherpad-lite ./

# install node dependencies for Etherpad
RUN bin/installDeps.sh \
    &&	rm -rf ~/.npm/_cacache

# plugins to install while building the container. By default no plugins are
# installed.
# If given a value, it has to be a space-separated, quoted list of plugin names.
#
# EXAMPLE:
#   ETHERPAD_PLUGINS="ep_codepad ep_author_neat"
ARG ETHERPAD_PLUGINS="ep_headings2 ep_align ep_comments_page ep_markdown ep_author_hover ep_font_color ep_adminpads2 ep_embedded_hyperlinks2 ep_print ep_mypads ep_set_title_on_pad ep_activepads"
# Install the plugins, if ETHERPAD_PLUGINS is not empty.
#
# Bash trick: in the for loop ${ETHERPAD_PLUGINS} is NOT quoted, in order to be
# able to split at spaces.
RUN for PLUGIN_NAME in ${ETHERPAD_PLUGINS}; do npm install "${PLUGIN_NAME}" || exit 1; done

# Copy the configuration file.
COPY --chown=etherpad:0 ./etherpad-lite/settings.json.docker /opt/etherpad-lite/settings.json

# Fix permissions for root group
RUN chmod -R g=u .

EXPOSE 9001
CMD ["node", "--experimental-worker", "node_modules/ep_etherpad-lite/node/server.js"]
