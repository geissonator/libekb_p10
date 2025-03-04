AM_CPPFLAGS  = -DFAPI2_ENABLE_PLATFORM_GET_TARGET
AM_MAKEFLAGS = --no-print-directory

ACLOCAL_AMFLAGS = -Im4
ARFLAGS = crDPST

EKB = $(srcdir)/ekb

ATTRIB_DIR = ./hwpf/fapi2/include/attributes
ATTRIB_HEADER = \
	$(ATTRIB_DIR)/attribute_ids.H \
	$(ATTRIB_DIR)/attribute_plat_check.H \
	$(ATTRIB_DIR)/fapi2AttrOverrideData.H \
	$(ATTRIB_DIR)/fapi2AttrOverrideEnums.H \
	$(ATTRIB_DIR)/fapi2AttrSyncData.H \
	$(ATTRIB_DIR)/fapi2_chip_ec_feature.H

ATTRIB_XML = \
	$(EKB)/hwpf/fapi2/xml/attribute_info/chip_attributes.xml \
	$(EKB)/hwpf/fapi2/xml/attribute_info/common_attributes.xml \
	$(EKB)/hwpf/fapi2/xml/attribute_info/scratch_attributes.xml \
	$(EKB)/hwpf/fapi2/xml/attribute_info/system_attributes.xml \
	$(EKB)/hwpf/fapi2/xml/attribute_info/unit_attributes.xml \
\
	$(EKB)/chips/p10/procedures/xml/attribute_info/p10_bars_attributes.xml \
	$(EKB)/chips/p10/procedures/xml/attribute_info/p10_chip_ec_attributes.xml \
	$(EKB)/chips/p10/procedures/xml/attribute_info/p10_clock_attributes.xml \
	$(EKB)/chips/p10/procedures/xml/attribute_info/p10_freq_attributes.xml \
	$(EKB)/chips/p10/procedures/xml/attribute_info/p10_hcode_image_build_attributes.xml \
	$(EKB)/chips/p10/procedures/xml/attribute_info/p10_ipl_attributes.xml \
	$(EKB)/chips/p10/procedures/xml/attribute_info/p10_ipl_customize_attributes.xml \
	$(EKB)/chips/p10/procedures/xml/attribute_info/p10_memory_bars_attributes.xml \
	$(EKB)/chips/p10/procedures/xml/attribute_info/p10_nest_attributes.xml \
	$(EKB)/chips/p10/procedures/xml/attribute_info/p10_pervasive_attributes.xml \
	$(EKB)/chips/p10/procedures/xml/attribute_info/p10_qme_attributes.xml \
	$(EKB)/chips/p10/procedures/xml/attribute_info/p10_runn_attributes.xml \
	$(EKB)/chips/p10/procedures/xml/attribute_info/p10_sbe_load_bootloader_attributes.xml \
	$(EKB)/chips/p10/procedures/xml/attribute_info/p10_sbe_attributes.xml \
	$(EKB)/chips/p10/procedures/xml/attribute_info/pm_plat_attributes.xml


$(ATTRIB_HEADER): $(ATTRIB_XML)
	@$(MKDIR_P) $(ATTRIB_DIR)
	$(EKB)/hwpf/fapi2/tools/parseAttributeInfo.pl --output-dir=$(ATTRIB_DIR) $(ATTRIB_XML)

$(ATTRIB_DIR)/platform_attrs.h: p10_attributes.db
	@$(MKDIR_P) $(ATTRIB_DIR)
	$(AM_V_GEN)$(srcdir)/scripts/attribute.py header $< $@

# Error info headers cannot be generated with parallel run
.NOTPARALLEL:

ERROR_INFO_XML = $(EKB)/chips/p10/procedures/xml/error_info/*.xml
ERROR_INFO_DIR = ./hwpf/fapi2/include/error_info
ERROR_INFO_HEADER = \
	$(ERROR_INFO_DIR)/hwp_ffdc_classes.H \
	$(ERROR_INFO_DIR)/hwp_error_info.H \
	$(ERROR_INFO_DIR)/hwp_return_codes.H \
	$(ERROR_INFO_DIR)/set_sbe_error_funcs.H \
	$(ERROR_INFO_DIR)/set_sbe_error.H

$(ERROR_INFO_HEADER) $(ERROR_INFO_DIR)/collect_reg_ffdc_regs.C: $(ERROR_INFO_XML)
	@$(MKDIR_P) $(ERROR_INFO_DIR)
	$(EKB)/hwpf/fapi2/tools/parseErrorInfo_p10.pl --use-variable-buffers --output-dir=$(ERROR_INFO_DIR) $(ERROR_INFO_XML)

#The PLAT HWP Error Parser file generated from Error XML files
ERROR_PARSER_XML = \
	$(EKB)/chips/p10/procedures/xml/error_info/p10_adu_errors.xml \
	$(EKB)/chips/p10/procedures/xml/error_info/p10_block_wakeup_intr_errors.xml \
	$(EKB)/chips/p10/procedures/xml/error_info/p10_clock_test_errors.xml \
	$(EKB)/chips/p10/procedures/xml/error_info/p10_determine_eco_mode_errors.xml \
	$(EKB)/chips/p10/procedures/xml/error_info/p10_do_fw_hb_istep.xml \
	$(EKB)/chips/p10/procedures/xml/error_info/p10_extract_sbe_rc_errors.xml \
	$(EKB)/chips/p10/procedures/xml/error_info/p10_fbc_core_topo_errors.xml \
	$(EKB)/chips/p10/procedures/xml/error_info/p10_getputsram_errors.xml \
	$(EKB)/chips/p10/procedures/xml/error_info/p10_hcd_cache_repair_initf.xml \
	$(EKB)/chips/p10/procedures/xml/error_info/p10_hcd_cache_startclocks_errors.xml \
	$(EKB)/chips/p10/procedures/xml/error_info/p10_hcd_cache_stopclocks_errors.xml \
	$(EKB)/chips/p10/procedures/xml/error_info/p10_hcd_chtm_purge.xml \
	$(EKB)/chips/p10/procedures/xml/error_info/p10_hcd_core_repair_initf.xml \
	$(EKB)/chips/p10/procedures/xml/error_info/p10_hcd_core_shadows_disable.xml \
	$(EKB)/chips/p10/procedures/xml/error_info/p10_hcd_core_shadows_enable.xml \
	$(EKB)/chips/p10/procedures/xml/error_info/p10_hcd_core_startclocks_errors.xml \
	$(EKB)/chips/p10/procedures/xml/error_info/p10_hcd_core_stopclocks_errors.xml \
	$(EKB)/chips/p10/procedures/xml/error_info/p10_hcd_core_vmin_disable.xml \
	$(EKB)/chips/p10/procedures/xml/error_info/p10_hcd_core_vmin_enable.xml \
	$(EKB)/chips/p10/procedures/xml/error_info/p10_hcd_corecache_clock_control_errors.xml \
	$(EKB)/chips/p10/procedures/xml/error_info/p10_hcd_corecache_power_control_errors.xml \
	$(EKB)/chips/p10/procedures/xml/error_info/p10_hcd_corecache_realign_errors.xml \
	$(EKB)/chips/p10/procedures/xml/error_info/p10_hcd_l2_purge.xml \
	$(EKB)/chips/p10/procedures/xml/error_info/p10_hcd_l3_purge.xml \
	$(EKB)/chips/p10/procedures/xml/error_info/p10_hcd_ncu_purge.xml \
	$(EKB)/chips/p10/procedures/xml/error_info/p10_hcd_powerbus_purge.xml \
	$(EKB)/chips/p10/procedures/xml/error_info/p10_io_init_done_errors.xml \
	$(EKB)/chips/p10/procedures/xml/error_info/p10_io_init_start_ppe_errors.xml \
	$(EKB)/chips/p10/procedures/xml/error_info/p10_io_iohs_poll_recal_errors.xml \
	$(EKB)/chips/p10/procedures/xml/error_info/p10_io_lib_errors.xml \
	$(EKB)/chips/p10/procedures/xml/error_info/p10_io_load_ppe_errors.xml \
	$(EKB)/chips/p10/procedures/xml/error_info/p10_io_power_errors.xml \
	$(EKB)/chips/p10/procedures/xml/error_info/p10_io_tdr_errors.xml \
	$(EKB)/chips/p10/procedures/xml/error_info/p10_iohs_reset.xml \
	$(EKB)/chips/p10/procedures/xml/error_info/p10_l3_flush_errors.xml \
	$(EKB)/chips/p10/procedures/xml/error_info/p10_load_iop_xram_errors.xml \
	$(EKB)/chips/p10/procedures/xml/error_info/p10_omi_reset_errors.xml \
	$(EKB)/chips/p10/procedures/xml/error_info/p10_pba_errors.xml \
	$(EKB)/chips/p10/procedures/xml/error_info/p10_perv_sbe_cmn_errors.xml \
	$(EKB)/chips/p10/procedures/xml/error_info/p10_pm_ocb_indir_access_errors.xml \
	$(EKB)/chips/p10/procedures/xml/error_info/p10_pm_ocb_init_errors.xml \
	$(EKB)/chips/p10/procedures/xml/error_info/p10_ppe_common_errors.xml \
	$(EKB)/chips/p10/procedures/xml/error_info/p10_ppe_state_errors.xml \
	$(EKB)/chips/p10/procedures/xml/error_info/p10_query_mssinfo_errors.xml \
	$(EKB)/chips/p10/procedures/xml/error_info/p10_ram_errors.xml \
	$(EKB)/chips/p10/procedures/xml/error_info/p10_read_write_iop_xram_errors.xml \
	$(EKB)/chips/p10/procedures/xml/error_info/p10_sbe_check_quiesce_errors.xml \
	$(EKB)/chips/p10/procedures/xml/error_info/p10_sbe_chiplet_init_errors.xml \
	$(EKB)/chips/p10/procedures/xml/error_info/p10_sbe_chiplet_pll_initf_errors.xml \
	$(EKB)/chips/p10/procedures/xml/error_info/p10_sbe_chiplet_pll_setup_errors.xml \
	$(EKB)/chips/p10/procedures/xml/error_info/p10_sbe_common_errors.xml \
	$(EKB)/chips/p10/procedures/xml/error_info/p10_sbe_core_spr_setup_errors.xml \
	$(EKB)/chips/p10/procedures/xml/error_info/p10_sbe_exit_cache_contained_errors.xml \
	$(EKB)/chips/p10/procedures/xml/error_info/p10_sbe_fabricinit_errors.xml \
	$(EKB)/chips/p10/procedures/xml/error_info/p10_sbe_i2c_errors.xml \
	$(EKB)/chips/p10/procedures/xml/error_info/p10_sbe_load_bootloader_errors.xml \
	$(EKB)/chips/p10/procedures/xml/error_info/p10_sbe_lpc_init_errors.xml \
	$(EKB)/chips/p10/procedures/xml/error_info/p10_sbe_mcs_setup_errors.xml \
	$(EKB)/chips/p10/procedures/xml/error_info/p10_sbe_npll_setup_errors.xml \
	$(EKB)/chips/p10/procedures/xml/error_info/p10_sbe_plat_errors.xml \
	$(EKB)/chips/p10/procedures/xml/error_info/p10_sbe_powerdown_backing_caches_error.xml \
	$(EKB)/chips/p10/procedures/xml/error_info/p10_sbe_rcs_setup_errors.xml \
	$(EKB)/chips/p10/procedures/xml/error_info/p10_sbe_ring_errors.xml \
	$(EKB)/chips/p10/procedures/xml/error_info/p10_sbe_scominit_errors.xml \
	$(EKB)/chips/p10/procedures/xml/error_info/p10_sbe_scratch_regs_errors.xml \
	$(EKB)/chips/p10/procedures/xml/error_info/p10_sbe_select_ex_errors.xml \
	$(EKB)/chips/p10/procedures/xml/error_info/p10_sbe_spi_cmd_errors.xml \
	$(EKB)/chips/p10/procedures/xml/error_info/p10_sbe_tp_chiplet_reset_errors.xml \
	$(EKB)/chips/p10/procedures/xml/error_info/p10_sbe_tracearray_errors.xml \
	$(EKB)/chips/p10/procedures/xml/error_info/p10_scomt_errors.xml \
	$(EKB)/chips/p10/procedures/xml/error_info/p10_sim_model_boot_errors.xml \
	$(EKB)/chips/p10/procedures/xml/error_info/p10_sim_post_chiplet_pll_setup.xml \
	$(EKB)/chips/p10/procedures/xml/error_info/p10_sim_pre_chiplet_pll_setup.xml \
	$(EKB)/chips/p10/procedures/xml/error_info/p10_sim_pre_io.xml \
	$(EKB)/chips/p10/procedures/xml/error_info/p10_smp_link_firs_errors.xml \
	$(EKB)/chips/p10/procedures/xml/error_info/p10_start_cbs_errors.xml \
	$(EKB)/chips/p10/procedures/xml/error_info/p10_thread_control_errors.xml

ERROR_PARSER_HEADER = \
	$(ERROR_INFO_DIR)/platHwpErrParser.H \
	$(ERROR_INFO_DIR)/platHwpErrParserFFDC.H

$(ERROR_PARSER_HEADER): $(ERROR_PARSER_XML)
	@$(MKDIR_P) $(ERROR_INFO_DIR)
	$(srcdir)/hwpf/fapi2/tools/platCreateHwpErrParser.pl --output-dir=$(ERROR_INFO_DIR) $(ERROR_PARSER_XML)

HWPF_HEADER = \
	$(srcdir)/hwpf/fapi2/include/hwp_executor.H \
	$(srcdir)/hwpf/fapi2/include/plat_attribute_service.H \
	$(srcdir)/hwpf/fapi2/include/plat/hw_access.H \
	$(srcdir)/hwpf/fapi2/include/plat/i2c_access.H \
	$(srcdir)/hwpf/fapi2/include/plat/mmio_access.H \
	$(srcdir)/hwpf/fapi2/include/plat/multicast.H \
	$(srcdir)/hwpf/fapi2/include/plat/plat_error_scope.H \
	$(srcdir)/hwpf/fapi2/include/plat/plat_hw_access.H \
	$(srcdir)/hwpf/fapi2/include/plat/plat_i2c_access.H \
	$(srcdir)/hwpf/fapi2/include/plat/plat_mbvpd_access.H \
	$(srcdir)/hwpf/fapi2/include/plat/plat_mmio_access.H \
	$(srcdir)/hwpf/fapi2/include/plat/plat_spd_access.H \
	$(srcdir)/hwpf/fapi2/include/plat/plat_target.H \
	$(srcdir)/hwpf/fapi2/include/plat/plat_trace.H \
	$(srcdir)/hwpf/fapi2/include/plat/plat_utils.H \
	$(srcdir)/hwpf/fapi2/include/plat/plat_error.H \
	$(srcdir)/hwpf/fapi2/include/plat/plat_vpd_access.H \
	$(srcdir)/hwpf/fapi2/include/plat/subroutine_executor.H \
	$(srcdir)/hwpf/fapi2/include/plat/target.H \
	$(srcdir)/hwpf/fapi2/include/plat/vpd_access.H \
	$(srcdir)/hwpf/fapi2/include/plat/plat_target_filter.H

p10_attributes.db: $(ATTRIB_XML) $(srcdir)/scripts/attribute.py
	$(AM_V_GEN)$(srcdir)/scripts/attribute.py parse $@ $(ATTRIB_XML)

BUILT_SOURCES = \
	$(ATTRIB_HEADER) \
	$(ATTRIB_DIR)/platform_attrs.h \
	$(ERROR_INFO_HEADER) \
	$(ERROR_INFO_DIR)/collect_reg_ffdc_regs.C \
	$(ERROR_PARSER_HEADER)

CLEANFILES = \
	$(ATTRIB_HEADER) \
	$(ATTRIB_DIR)/platform_attrs.h \
	$(ERROR_INFO_HEADER) \
	$(ERROR_INFO_DIR)/collect_reg_ffdc_regs.C \
	$(ERROR_PARSER_HEADER)

if BUILD_DB
data_DATA = p10_attributes.db
CLEANFILES += p10_attributes.db
endif

include Makefile.proc.am

OPTFLAGS = -Os -O2
LOCALCFLAGS = $(OPTFLAGS) -g -Wall -std=gnu11 $(TARGET_ENDIAN)

# Our own platform include files (hwpf/fapi2/include/plat) shoud
# appear before the ekb ones in this list as we need the compiler to
# choose some of ours. Specifically return_code_defs.H.
LOCALCXXFLAGS = $(OPTFLAGS) -Wall -std=gnu++11 \
		-fpermissive -fno-exceptions -fno-rtti \
		$(TARGET_ENDIAN) \
		-I$(ATTRIB_DIR) \
		-I$(ERROR_INFO_DIR) \
		-I$(srcdir) \
		-I$(srcdir)/src \
		-I$(srcdir)/hwpf/fapi2/include \
		-I$(srcdir)/hwpf/fapi2/include/plat \
		-I$(srcdir)/ekb/hwpf/fapi2/include \
		-I$(srcdir)/ekb/chips/p10/common/include \
		-I$(srcdir)/ekb/chips/p10/procedures/hwp/ffdc \
		-I$(srcdir)/ekb/chips/common/utils/scomt \
		-I$(srcdir)/ekb/chips/ocmb/explorer/common/include \
		-I$(srcdir)/ekb/chips/ocmb/odyssey/common/include \
		$(PROC_INCLUDE_CFLAGS)

lib_LTLIBRARIES = libekb.la
nobase_include_HEADERS = \
	$(EKB_HEADER) \
	$(ATTRIB_HEADER) \
	$(ATTRIB_DIR)/platform_attrs.h \
	$(ERROR_INFO_HEADER) \
	$(HWPF_HEADER) \
	hwpf/fapi2/include/hwp_pel_data.H \
	$(ERROR_PARSER_HEADER)

include_HEADERS = libekb.H

libekb_la_SOURCES = $(PROCEDURES) \
		    $(EKB_HEADER) \
		    libekb.C \
		    libekb.H \
		    hwpf/fapi2/src/fapi2_utils.C \
		    hwpf/fapi2/src/plat/plat_utils.C \
		    hwpf/fapi2/src/plat/plat_error.C \
		    hwpf/fapi2/src/plat/target.C \
		    ekb/hwpf/fapi2/src/error_info.C \
		    ekb/hwpf/fapi2/src/ffdc.C \
		    $(ATTRIB_HEADER) \
		    $(ATTRIB_DIR)/platform_attrs.h \
		    $(ERROR_INFO_HEADER) \
		    hwpf/fapi2/include/error_info/collect_reg_ffdc_regs.C \
		    $(HWPF_HEADER) \
		    $(ERROR_PARSER_HEADER)

libekb_la_CXXFLAGS = $(LOCALCXXFLAGS)
libekb_la_LDFLAGS = -version-info $(SONAME_CURRENT):$(SONAME_REVISION):$(SONAME_AGE)

$(PROCEDURES): $(ATTRIB_HEADER) \
	       $(ATTRIB_DIR)/platform_attrs.h \
	       $(ERROR_INFO_HEADER)
