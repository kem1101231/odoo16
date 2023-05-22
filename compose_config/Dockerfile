FROM ubuntu:20.04
ARG DEBIAN_FRONTEND=noninteractive
RUN apt-get update \
	&& apt-get install -y --no-install-recommends \
                        tzdata \
						git \
						python3 \
						python3-pip \
						build-essential \
						wget \
						python3-dev \
						python3-venv \
						python3-wheel \
						libxslt-dev \
						libzip-dev \
						libldap2-dev \
						libsasl2-dev \
						python3-setuptools \
						node-less \
						libjpeg-dev \
						gdebi \
						libpq-dev \
						python-dev \
						libxml2-dev \
						libxslt1-dev \
						libldap2-dev \
						libsasl2-dev \
						libffi-dev \
						nodejs \
						npm \
						wget \
						dpkg \
						zip \
						unzip \
						tar \
                        xfonts-base \
						xfonts-75dpi 
                        


RUN npm install -g rtlcss 

	#RUN ln -s /usr/bin/nodejs /usr/bin/node \
	#RUN npm install -g less@3.0.4 less-plugin-clean-css \

    

RUN adduser --system --home=/opt/odoo --group odoo 
RUN mkdir /var/log/odoo 
RUN chown -R odoo:root /var/log/odoo 
RUN mkdir /etc/odoo 
	
    #RUN wget https://pypi.python.org/packages/a8/70/bd554151443fe9e89d9a934a7891aaffc63b9cb5c7d608972919a002c03c/gdata-2.0.18.tar.gz 
	#RUN tar zxvf gdata-2.0.18.tar.gz 
	#RUN chown -R odoo: gdata-2.0.18 \
	#RUN cd gdata-2.0.18/ \
	#RUN python setup.py install \
	#RUN pip install Pillow==3.4.0 \
    
RUN git clone --depth 1 --branch 16.0 https://www.github.com/odoo/odoo /opt/odoo/odoo-16 
RUN pip3 install -r /opt/odoo/odoo-16/requirements.txt

RUN wget https://github.com/wkhtmltopdf/packaging/releases/download/0.12.6-1/wkhtmltox_0.12.6-1.bionic_amd64.deb 
RUN dpkg -i wkhtmltox_0.12.6-1.bionic_amd64.deb 
RUN cp /usr/local/bin/wkhtmltoimage  /usr/bin/wkhtmltoimage 
RUN cp /usr/local/bin/wkhtmltopdf  /usr/bin/wkhtmltopdf

COPY ./compose_config/odoo-server.conf /etc/odoo/
COPY ./external_addons/. /opt/odoo/external_addons/

RUN chown -R odoo: /opt/odoo/ \
     && chown odoo:root /var/log/odoo \
     && chown odoo: /etc/odoo/odoo-server.conf \
     && chmod 640 /etc/odoo/odoo-server.conf

RUN pip3 install -r /opt/odoo/external_addons/requirements.txt

USER odoo

CMD ["python3 /opt/odoo/odoo-16/odoo-bin -c /etc/odoo/odoo-server.conf"]

WORKDIR /opt/odoo
