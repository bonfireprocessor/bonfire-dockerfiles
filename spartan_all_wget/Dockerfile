FROM gassettj/papilio-environment-cloud9:latest

RUN apt-get update && apt-get install -y lua5.1 luarocks ssh curl \
&& luarocks install luafilesystem  \
&& luarocks install  lpack \
&& luarocks install  md5 \
&& luarocks install  bit32

RUN  curl -SL https://github.com/gnu-mcu-eclipse/riscv-none-gcc/releases/download/v7.2.0-2-20180110/gnu-mcu-eclipse-riscv-none-gcc-7.2.0-2-20180111-2230-centos64.tgz \
    | tar -xzC /opt \
    && ln -s /opt/gnu-mcu-eclipse/riscv-none-gcc/7.2.0-2-20180111-2230 /opt/riscv



RUN apt-get install -y libgnat-4.9 \
    && mkdir -p /opt/ghdl  \
    && curl -SL https://github.com/ghdl/ghdl/releases/download/v0.34/ghdl-v0.34-mcode-ubuntu.tgz \
    | tar -xzC /opt/ghdl
    

ENV PATH="${PATH}:/opt/riscv/bin:/opt/ghdl/bin" TARGET_PREFIX="riscv-none-embed"


WORKDIR /cloud9
RUN rm -rf fusesoc && git clone https://github.com/ThomasHornschuh/fusesoc.git 
#RUN rm -rf fusesoc && git clone https://github.com/olofk/fusesoc.git
WORKDIR /cloud9/fusesoc
RUN git checkout tags/BONFIRE && pip install -e . 
#RUN git checkout bmm_support && pip install -e . 
ADD fusesoc.conf /root/.config/fusesoc/fusesoc.conf


ADD Xilinx.lic /root/.Xilinx/Xilinx.lic 

WORKDIR /

