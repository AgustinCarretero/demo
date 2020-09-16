def get_data_for_Dominion_monthly_data_report(SiteAssetID,start,stop,resolution):
        
    # print('\tGetting GHI data.')
    # GHI_data_15min = get_X_min_avg_GHI_data(SiteAssetID,start,stop,resolution)
    # GHI_data_15min = format_data_for_Dominion_monthly_data_report(GHI_data_15min,pivot_values_str='GHIIrradiance')
    
    print('\tGetting POA data.')
    POA_data_15min = get_X_min_avg_POA_data(SiteAssetID,start,stop,resolution)
    POA_data_15min = format_data_for_Dominion_monthly_data_report(POA_data_15min,pivot_values_str='POAIrradiance')

    print('\tGetting Tamb data.')
    Tamb_data_15min = get_X_min_avg_Tamb_data(SiteAssetID,start,stop,resolution)
    Tamb_data_15min = format_data_for_Dominion_monthly_data_report(Tamb_data_15min,pivot_values_str='TemperatureC')
    
    # print('\tGetting WindSpeed data.')
    # WindSpeed_data_15min = get_X_min_avg_WindSpeed_data(SiteAssetID,start,stop,resolution)
    # WindSpeed_data_15min = format_data_for_Dominion_monthly_data_report(WindSpeed_data_15min,pivot_values_str='WindSpeedMpS')

    # print('\tGetting RelativeHumidity data.')
    # RelativeHumidity_data_15min = get_X_min_avg_RelativeHumidity_data(SiteAssetID,start,stop,resolution)
    # RelativeHumidity_data_15min = format_data_for_Dominion_monthly_data_report(RelativeHumidity_data_15min,pivot_values_str='RelativeHumidity')
    
    # try:
    #     print('\tGetting Rain data.')
    #     Rain_data_15min = get_X_min_sum_Rain_data(SiteAssetID,start,stop,resolution)
    #     Rain_data_15min = format_data_for_Dominion_monthly_data_report(Rain_data_15min,pivot_values_str='RainFallmm')
    # except:
    #     print('\t No Rain Data.')
    
    print('\tGetting Meter KWTotal data.')
    Meter_data_15min = get_X_min_avg_Meter_data(SiteAssetID,start,stop,resolution)
    Meter_data_15min = format_data_for_Dominion_monthly_data_report(Meter_data_15min,
                                                                    pivot_index=None,
                                                                    pivot_values_str='kWTotal')
    
    print('\tGetting Meter kWhReceived data.')
    Meter_kWh_data_15min = get_X_min_avg_Meter_data(SiteAssetID,start,stop,resolution)
    Meter_kWh_data_15min = format_data_for_Dominion_monthly_data_report(Meter_kWh_data_15min,
                                                                    pivot_index=None,
                                                                    pivot_values_str='kWhReceived')
    
    print('\tGetting InverterAC data.')
    inv_data_raw = get_generic_table_time_series('vw60PerformanceInverters', SiteAssetID, start, stop, columns='ACOutputKW, DCInputKW')
    # pivot by inverter
    InverterAC_data_15min = inv_data_raw.pivot_table(index = inv_data_raw.index, columns='AssetID', values='ACOutputKW').resample(f'{resolution}min').mean()
    # get AssetTitles
    inv_metadata = get_generic_table('vwInverters', SiteAssetID, columns='AssetTitle')
    # replace AssetID column headers with AssetTitle
    InverterAC_data_15min.columns = inv_metadata.merge(InverterAC_data_15min.columns.to_frame(index=False)).AssetTitle
    

    # print('\tGetting InverterDC data.')
    # # pivot by inverter
    # InverterDC_data_15min = inv_data_raw.pivot_table(index = inv_data_raw.index, columns='AssetID', values='ACOutputKW').resample(f'{resolution}min').mean()
    # # replace AssetID column headers with AssetTitle
    # InverterDC_data_15min.columns = inv_metadata.merge(InverterDC_data_15min.columns.to_frame(index=False)).AssetTitle

    data_dict = {
        #'GHIData': GHI_data_15min,
                'POAData': POA_data_15min,
                'TambData': Tamb_data_15min,
         #       'WSData': WindSpeed_data_15min,
         #       'RHData': RelativeHumidity_data_15min,
         #       'RainData': Rain_data_15min,
                'MeterData': Meter_data_15min,
                'MeterkWhData': Meter_kWh_data_15min,
                'InverterACData':InverterAC_data_15min,
        #       'InverterDCData':InverterDC_data_15min
                }
    
    return data_dict