idf_build_get_property(target IDF_TARGET)

set(srcs "")
set(includes "")

if(CONFIG_SOC_ULP_SUPPORTED OR CONFIG_SOC_RISCV_COPROC_SUPPORTED)

    list(APPEND srcs
        "ulp_common/ulp_common.c")

    list(APPEND includes
        ulp_common/include
        ulp_common/include/${target})

    if(CONFIG_ULP_COPROC_TYPE_FSM)
        list(APPEND srcs
            "ulp_fsm/ulp.c"
            "ulp_fsm/ulp_macro.c")

            list(APPEND includes
                ulp_fsm/include)

    elseif(CONFIG_ULP_COPROC_TYPE_RISCV)
        list(APPEND srcs
            "ulp_riscv/ulp_riscv.c")

        list(APPEND includes
            ulp_riscv/include)
    endif()
endif()

idf_component_register(SRCS ${srcs}
                       INCLUDE_DIRS ${includes})
