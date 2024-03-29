# Compile flow 

sudo bash kitware-archive.sh

west init ./zephyrproject

cd ./zephyrproject

west update

west zephyr-export

pip3 install -r ./zephyr/scripts/requirements.txt

cd ..

## download SDK

wget https://github.com/zephyrproject-rtos/sdk-ng/releases/download/v0.15.2/zephyr-sdk-0.15.2_linux-x86_64.tar.gz

wget -O - https://github.com/zephyrproject-rtos/sdk-ng/releases/download/v0.15.2/sha256.sum | shasum --check --ignore-missing

tar xvf zephyr-sdk-0.15.2_linux-x86_64.tar.gz

cd zephyr-sdk-0.15.2

./setup.sh

cd zephyrproject/zephyr/

west build -p always -b  arduino_due samples/basic/blinky

west build -p always -b ast1030_evb  samples/hello_world

## use qemu to run ast1030 image

qemu-system-arm -M ast1030-evb -nographic -kernel zephyr.elf

wget https://jenkins.openbmc.org/job/latest-qemu-x86/lastSuccessfulBuild/artifact/qemu/build/qemu-system-arm


west build -p always -b ast1030_evb  samples/basic/minimal/

west build -p always -b qemu_x86_64  samples/basic/minimal/

## qemu m3 
west build -b qemu_cortex_m3 samples/synchronization
west build -t run

## qemu x86 
export OVMF_FD_PATH=/usr/share/edk2.git/ovmf-x64/OVMF_CODE-pure-efi.fd
west build -b qemu_x86_64 -p auto samples/hello_world/ -DCONF_FILE=prj_uefi.conf
west build -t run

## Board List
### arc:

  em_starterkit  
  em_starterkit_em11d  
  em_starterkit_em7d  
  em_starterkit_em7d_v22  
  emsdp  
  emsdp_em4  
  emsdp_em5d
  emsdp_em6  
  emsdp_em7d  
  emsdp_em7d_esp  
  emsdp_em9d
  
  hsdk  
  hsdk_2cores
  
  iotdk
  
  nsim_em  
  nsim_em11d  
  nsim_em7d_v22  
  nsim_hs  
  nsim_hs5x  
  nsim_hs5x_smp  
  nsim_hs6x  
  nsim_hs6x_smp  
  nsim_hs_flash_xip  
  nsim_hs_mpuv6  
  nsim_hs_smp  
  nsim_hs_sram  
  nsim_sem  
  nsim_sem_mpu_stack_guard
  
  qemu_arc_em  
  qemu_arc_hs  
  qemu_arc_hs5x  
  qemu_arc_hs6x  
  qemu_arc_hs_xip
  
### arm:
  96b_aerocore2  
  96b_argonkey  
  96b_avenger96  
  96b_carbon  
  96b_carbon_nrf51  
  96b_meerkat96  
  96b_neonkey  
  96b_nitrogen  
  96b_stm32_sensor_mez  
  96b_wistrio
  
  actinius_icarus  
  actinius_icarus_bee  
  actinius_icarus_bee_ns  
  actinius_icarus_ns  
  actinius_icarus_som  
  actinius_icarus_som_dk  
  actinius_icarus_som_dk_ns  
  actinius_icarus_som_ns  
  adafruit_feather_m0_basic_proto  
  adafruit_feather_m0_lora  
  adafruit_feather_nrf52840  
  adafruit_feather_stm32f405  
  adafruit_itsybitsy_m4_express  
  adafruit_itsybitsy_nrf52840  
  adafruit_kb2040  
  adafruit_trinket_m0  
  arduino_due  
  arduino_giga_r1_m4  
  arduino_giga_r1_m7  
  arduino_mkrzero  
  arduino_nano_33_ble  
  arduino_nano_33_ble_sense  
  arduino_nano_33_iot  
  arduino_nicla_sense_me  
  arduino_portenta_h7_m4  
  arduino_portenta_h7_m7  
  arduino_zero  
  arty_a7_arm_designstart_m1  
  arty_a7_arm_designstart_m3  
  ast1030_evb  
  atsamc21n_xpro  
  atsamd20_xpro  
  atsamd21_xpro  
  atsame54_xpro  
  atsaml21_xpro  
  atsamr21_xpro  
  atsamr34_xpro
  
  b_g474e_dpow1  
  b_l072z_lrwan1  
  b_l4s5i_iot01a  
  b_u585i_iot02a  
  b_u585i_iot02a_ns  
  bbc_microbit  
  bbc_microbit_v2  
  bcm958401m2  
  bcm958402m2_m7  
  bl5340_dvk_cpuapp  
  bl5340_dvk_cpuapp_ns  
  bl5340_dvk_cpunet  
  bl652_dvk  
  bl653_dvk  
  bl654_dvk4  
  bl654_sensor_board  
  bl654_usb  
  black_f407ve  
  black_f407zg_pro  
  blackpill_f401cc  
  blackpill_f401ce  
  blackpill_f411ce  
  blueclover_plt_demo_v2_nrf52832  
  bt510  
  bt610
  
  cc1352p1_launchxl  
  cc1352r1_launchxl  
  cc1352r_sensortag  
  cc26x2r1_launchxl  
  cc3220sf_launchxl  
  cc3235sf_launchxl  
  circuitdojo_feather_nrf9160  
  circuitdojo_feather_nrf9160_ns  
  colibri_imx7d_m4  
  contextualelectronics_abc  
  cy8ckit_062_ble_m0  
  cy8ckit_062_ble_m4  
  cy8ckit_062_wifi_bt_m0  
  cy8ckit_062_wifi_bt_m4  
  cy8cproto_062_4343w  
  cyclonev_socdk
  
  da1469x_dk_pro  
  decawave_dwm1001_dev  
  degu_evk  
  disco_l475_iot1  
  dragino_lsn50  
  dragino_nbsn95
  
  ebyte_e73_tbb_nrf52832  
  efm32gg_slwstk6121a  
  efm32gg_stk3701a  
  efm32hg_slstk3400a  
  efm32pg_stk3401a  
  efm32pg_stk3402a  
  efm32pg_stk3402a_jg  
  efm32wg_stk3800  
  efr32_radio_brd4104a  
  efr32_radio_brd4180a  
  efr32_radio_brd4250b  
  efr32_radio_brd4255a  
  efr32bg_sltb010a  
  efr32mg_sltb004a
  
  faze  
  frdm_k22f  
  frdm_k64f  
  frdm_k82f  
  frdm_kl25z  
  frdm_kw41z  
  fvp_baser_aemv8r_aarch32
  
  gd32a503v_eval  
  gd32e103v_eval
  gd32e507v_start
  gd32e507z_eval
  gd32f350r_eval
  gd32f403z_eval
  gd32f407v_start
  gd32f450i_eval
  gd32f450v_start
  gd32f450z_eval
  gd32f470i_eval
  gd32l233r_eval
  google_dragonclaw
  google_kukui
  hexiwear_k64
  hexiwear_kw40z
  holyiot_yj16019
  ip_k66f
  legend
  lora_e5_dev_board
  lpcxpresso11u68
  lpcxpresso51u68
  lpcxpresso54114_m0
  lpcxpresso54114_m4
  lpcxpresso55s06
  lpcxpresso55s16
  lpcxpresso55s28
  lpcxpresso55s36
  lpcxpresso55s69_cpu0
  lpcxpresso55s69_cpu1
  lpcxpresso55s69_ns
  mec1501modular_assy6885
  mec15xxevb_assy6853
  mec172xevb_assy6906
  mec172xmodular_assy6930
  mec2016evb_assy6797
  mercury_xu
  mg100
  mikroe_clicker_2
  mikroe_mini_m4_for_stm32
  mimx8mm_evk
  mimx8mp_evk_ddr
  mimx8mp_evk_itcm
  mimx8mq_evk_cm4
  mimxrt1010_evk
  mimxrt1015_evk
  mimxrt1020_evk
  mimxrt1024_evk
  mimxrt1050_evk
  mimxrt1050_evk_qspi
  mimxrt1060_evk
  mimxrt1060_evk_hyperflash
  mimxrt1060_evkb
  mimxrt1064_evk
  mimxrt1160_evk_cm4
  mimxrt1160_evk_cm7
  mimxrt1170_evk_cm4
  mimxrt1170_evk_cm7
  mimxrt595_evk_cm33
  mimxrt685_evk_cm33
  mm_feather
  mm_swiftio
  mps2_an385
  mps2_an521
  mps2_an521_ns
  mps2_an521_remote
  mps3_an547
  mps3_an547_ns
  msp_exp432p401r_launchxl
  npcx7m6fb_evb
  npcx9m6f_evb
  nrf21540dk_nrf52840
  nrf51_ble400
  nrf51_blenano
  nrf51_vbluno51
  nrf51dk_nrf51422
  nrf51dongle_nrf51422
  nrf52832_mdk
  nrf52833dk_nrf52820
  nrf52833dk_nrf52833
  nrf52840_blip
  nrf52840_mdk
  nrf52840_mdk_usb_dongle
  nrf52840_papyr
  nrf52840dk_nrf52811
  nrf52840dk_nrf52840
  nrf52840dongle_nrf52840
  nrf52_adafruit_feather
  nrf52_blenano2
  nrf52_sparkfun
  nrf52_vbluno52
  nrf52dk_nrf52805
  nrf52dk_nrf52810
  nrf52dk_nrf52832
  nrf5340_audio_dk_nrf5340_cpuapp
  nrf5340_audio_dk_nrf5340_cpuapp_ns
  nrf5340_audio_dk_nrf5340_cpunet
  nrf5340dk_nrf5340_cpuapp
  nrf5340dk_nrf5340_cpuapp_ns
  nrf5340dk_nrf5340_cpunet
  nrf9160_innblue21
  nrf9160_innblue21_ns
  nrf9160_innblue22
  nrf9160_innblue22_ns
  nrf9160dk_nrf52840
  nrf9160dk_nrf9160
  nrf9160dk_nrf9160_ns
  nucleo_c031c6
  nucleo_f030r8
  nucleo_f031k6
  nucleo_f042k6
  nucleo_f070rb
  nucleo_f091rc
  nucleo_f103rb
  nucleo_f207zg
  nucleo_f302r8
  nucleo_f303k8
  nucleo_f303re
  nucleo_f334r8
  nucleo_f401re
  nucleo_f410rb
  nucleo_f411re
  nucleo_f412zg
  nucleo_f413zh
  nucleo_f429zi
  nucleo_f446re
  nucleo_f446ze
  nucleo_f746zg
  nucleo_f756zg
  nucleo_f767zi
  nucleo_g031k8
  nucleo_g070rb
  nucleo_g071rb
  nucleo_g0b1re
  nucleo_g431rb
  nucleo_g474re
  nucleo_h723zg
  nucleo_h743zi
  nucleo_h745zi_q_m4
  nucleo_h745zi_q_m7
  nucleo_h753zi
  nucleo_h7a3zi_q
  nucleo_l011k4
  nucleo_l031k6
  nucleo_l053r8
  nucleo_l073rz
  nucleo_l152re
  nucleo_l412rb_p
  nucleo_l432kc
  nucleo_l433rc_p
  nucleo_l452re
  nucleo_l452re_p
  nucleo_l476rg
  nucleo_l496zg
  nucleo_l4a6zg
  nucleo_l4r5zi
  nucleo_l552ze_q
  nucleo_l552ze_q_ns
  nucleo_u575zi_q
  nucleo_wb55rg
  nucleo_wl55jc
  nuvoton_pfm_m487
  olimex_lora_stm32wl_devkit
  olimex_stm32_e407
  olimex_stm32_h103
  olimex_stm32_h405
  olimex_stm32_h407
  olimex_stm32_p405
  olimexino_stm32
  pan1770_evb
  pan1780_evb
  pan1781_evb
  pan1782_evb
  particle_argon
  particle_boron
  particle_xenon
  pico_pi_m4
  pinetime_devkit0
  pinnacle_100_dvk
  qemu_cortex_a9
  qemu_cortex_m0
  qemu_cortex_m3
  qemu_cortex_r5
  qomu
  quick_feather
  rak4631_nrf52840
  rak5010_nrf52840
  raytac_mdbt50q_db_33_nrf52833
  raytac_mdbt50q_db_40_nrf52840
  rcar_h3_salvatorx_cr7
  rcar_h3ulcb_cr7
  rddrone_fmuk66
  reel_board
  reel_board_v2
  rm1xx_dvk
  ronoth_lodev
  rpi_pico
  ruuvi_ruuvitag
  s32z270dc2_rtu0_r52
  s32z270dc2_rtu1_r52
  sam4e_xpro
  sam4l_ek
  sam4s_xplained
  sam_e70_xplained
  sam_e70b_xplained
  sam_v71_xult
  sam_v71b_xult
  scobc_module1
  seeeduino_xiao
  segger_trb_stm32f407
  sensortile_box
  serpente
  sparkfun_pro_micro_rp2040
  sparkfun_thing_plus_nrf9160
  sparkfun_thing_plus_nrf9160_ns
  steval_fcu001v1
  stm3210c_eval
  stm32373c_eval
  stm32_min_dev_black
  stm32_min_dev_blue
  stm32f030_demo
  stm32f072_eval
  stm32f072b_disco
  stm32f0_disco
  stm32f103_mini
  stm32f3_disco
  stm32f3_seco_d23
  stm32f401_mini
  stm32f411e_disco
  stm32f412g_disco
  stm32f429i_disc1
  stm32f469i_disco
  stm32f4_disco
  stm32f723e_disco
  stm32f746g_disco
  stm32f7508_dk
  stm32f769i_disco
  stm32g0316_disco
  stm32g071b_disco
  stm32g081b_eval
  stm32h735g_disco
  stm32h747i_disco_m4
  stm32h747i_disco_m7
  stm32h7b3i_dk
  stm32l1_disco
  stm32l476g_disco
  stm32l496g_disco
  stm32l562e_dk
  stm32l562e_dk_ns
  stm32mp157c_dk2
  stm32vl_disco
  swan_r5
  tdk_robokit1
  teensy40
  teensy41
  thingy52_nrf52832
  thingy53_nrf5340_cpuapp
  thingy53_nrf5340_cpuapp_ns
  thingy53_nrf5340_cpunet
  twr_ke18f
  twr_kv58f220m
  ubx_bmd300eval_nrf52832
  ubx_bmd330eval_nrf52810
  ubx_bmd340eval_nrf52840
  ubx_bmd345eval_nrf52840
  ubx_bmd360eval_nrf52811
  ubx_bmd380eval_nrf52840
  ubx_evkannab1_nrf52832
  ubx_evkninab1_nrf52832
  ubx_evkninab3_nrf52840
  ubx_evkninab4_nrf52833
  udoo_neo_full_m4
  usb_kw24d512
  v2m_beetle
  v2m_musca_b1
  v2m_musca_b1_ns
  v2m_musca_s1
  v2m_musca_s1_ns
  warp7_m4
  waveshare_open103z
  we_ophelia1ev_nrf52805
  we_proteus2ev_nrf52832
  we_proteus3ev_nrf52840
  wio_terminal
  xiao_ble
  xiao_ble_sense
  xmc45_relax_kit
  zybo
### arm64:
  bcm958402m2_a72
  fvp_base_revc_2xaemv8a
  fvp_base_revc_2xaemv8a_smp_ns
  fvp_baser_aemv8r
  fvp_baser_aemv8r_smp
  intel_socfpga_agilex_socdk
  khadas_edgev
  mimx8mm_evk_a53
  mimx8mm_evk_a53_smp
  mimx8mn_evk_a53
  mimx8mn_evk_a53_smp
  mimx8mp_evk_a53
  mimx8mp_evk_a53_smp
  mimx93_evk_a55
  nxp_ls1046ardb
  nxp_ls1046ardb_smp_2cores
  nxp_ls1046ardb_smp_4cores
  phycore_am62x_a53
  qemu_cortex_a53
  qemu_cortex_a53_smp
  qemu_cortex_a53_xip
  qemu_kvm_arm64
  xenvm
  xenvm_gicv3

### mips:
  qemu_malta
  qemu_malta_be
  
### nios2:
  altera_max10
  qemu_nios2
  
### posix:

  native_posix
  native_posix_64
  nrf52_bsim
### riscv:
  adp_xc7k_ae350
  beaglev_starlight_jh7100
  esp32c3_devkitm
  gd32vf103c_starter
  gd32vf103v_eval
  hifive1
  hifive1_revb
  hifive_unleashed
  hifive_unmatched
  icev_wireless
  it8xxx2_evb
  litex_vexriscv
  longan_nano
  longan_nano_lite
  m2gl025_miv
  mpfs_icicle
  neorv32
  niosv_m
  opentitan_earlgrey
  qemu_riscv32
  qemu_riscv32_smp
  qemu_riscv32_xip
  qemu_riscv32e
  qemu_riscv64
  qemu_riscv64_smp
  rv32m1_vega_ri5cy
  rv32m1_vega_zero_riscy
  sparkfun_red_v_things_plus
  stamp_c3
  tlsr9518adk80d
  xiao_esp32c3
  
### sparc:
  generic_leon3
  gr716a_mini
  qemu_leon3
  
### x86:
  acrn
  acrn_ehl_crb
  ehl_crb
  ehl_crb_sbl
  qemu_x86
  qemu_x86_64
  qemu_x86_64_nokpti
  qemu_x86_lakemont
  qemu_x86_nokpti
  qemu_x86_nommu
  qemu_x86_nopae
  qemu_x86_tiny
  qemu_x86_virt
  qemu_x86_xip
  rpl_crb
  up_squared
  
### xtensa:
  esp32
  esp32_ethernet_kit
  esp32_net
  esp32s2_franzininho
  esp32s2_saola
  esp32s3_devkitm
  esp_wrover_kit
  heltec_wifi_lora32_v2
  intel_adsp_ace15_mtpm
  intel_adsp_cavs15
  intel_adsp_cavs18
  intel_adsp_cavs20
  intel_adsp_cavs20_jsl
  intel_adsp_cavs25
  intel_adsp_cavs25_tgph
  m5stickc_plus
  nxp_adsp_imx8
  nxp_adsp_imx8m
  nxp_adsp_imx8x
  odroid_go
  olimex_esp32_evb
  qemu_xtensa
  xt-sim
