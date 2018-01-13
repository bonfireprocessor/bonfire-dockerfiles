FROM gassettj/papilio-environment-cloud9:latest

ADD Xilinx.lic /root/.Xilinx/Xilinx.lic 

WORKDIR /cloud9
RUN rm -rf fusesoc && git clone https://github.com/ThomasHornschuh/fusesoc.git 
#RUN rm -rf fusesoc && git clone https://github.com/olofk/fusesoc.git
WORKDIR /cloud9/fusesoc
RUN git checkout tags/BONFIRE && pip install -e . 
#RUN git checkout bmm_support && pip install -e . 
ADD fusesoc.conf /root/.config/fusesoc/fusesoc.conf


RUN apt-get update && apt-get install -y lua5.1 luarocks ssh \
&& luarocks install luafilesystem  \
&& luarocks install  lpack \
&& luarocks install  md5 \
&& luarocks install  bit32

ADD gnu-mcu-eclipse-riscv-none-gcc-7.2.0-1-20171109-1926-debian64.tgz  /opt
RUN ln -s /opt/gnu-mcu-eclipse/riscv-none-gcc/7.2.0-1-20171109-1926 /opt/riscv
ADD ghdl-0.33-x86_64-linux.tgz /opt/ghdl
ENV PATH="${PATH}:/opt/riscv/bin:/opt/ghdl/bin" TARGET_PREFIX="riscv-none-embed"

WORKDIR /

