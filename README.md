# MULTIVARIATE-ANALYSIS
IT CONTAINS SCATTER PLOT,CORRELATION,VIOLION PLOT,BOX PLOT

TO CREATE SCATTER PLOT BETWEEN TWO COLUMNS

     fig, ax = plt.subplots(figsize=(8,6))
     ax.scatter( df['TotalArea'],df['SalePrice'])
     ax.set_xlabel('TotalArea')
     ax.set_ylabel('SalePrice')
     plt.show()
     
 FOR CORRELATION GRAPH
 
     plt.figure(figsize=(10,10))
     corr = df.corr()
     sns.heatmap(corr)
     
 FOR CREATING MULTI GRAPHS IN A ROW 
 
    plt.figure(figsize=(22, 8))
    ax=plt.subplot(1, 3, 1)
    ax.scatter( df['OverallQual'],df['SalePrice'])
    plt.xlabel('OverallQual')
    plt.ylabel('SalePrice')
    plt.subplot(1, 3, 2)
    sns.boxplot(x='OverallQual',y='SalePrice',data=df)
    plt.subplot(1, 3, 3)
    sns.violinplot(x="OverallQual",y="SalePrice",data=df,size=8)
    plt.show()
    
    
FOR CREATING JOINT PLOT 

    sns.jointplot(x="OverallQual",y="SalePrice",data=df,kind='kde')
    
    
FOR CREATING TWO GRAPHS IN A ROW 

         plt.figure(figsize=(16, 4))
        ax=plt.subplot(1, 2, 1)
        ax.scatter( df['YearRemodAdd'],df['SalePrice'])
        plt.xlabel('YearRemodAdd')
        plt.ylabel('SalePrice')
        plt.subplot(1, 2, 2)
        sns.boxplot(x='YearRemodAdd',y='SalePrice',data=df)
        plt.show()
        
    
 BOXPLOTS OF CATEGORICAL COLUMNS WITH RESPECT TO SALEPRICE       
        
        def boxplot(x,y,**kwargs):
            sns.boxplot(x=x,y=y)
            x = plt.xticks(rotation=90)

            cat = [f for f in df.columns if df.dtypes[f] == 'object']

            p = pd.melt(df, id_vars='SalePrice', value_vars=cat)
            g = sns.FacetGrid (p, col='variable', col_wrap=2, sharex=False, sharey=False, size=5)
            g = g.map(boxplot, 'value','SalePrice')
            g
        
 VIOLIN PLOTS OF CATEGORICAL COLUMNS WITH RESPECT TO SALEPRICE   
 
 
    def violinplot(x,y,**kwargs):
            sns.violinplot(x=x,y=y)
            x = plt.xticks(rotation=90)

            cat = [f for f in df.columns if df.dtypes[f] == 'object']

            p = pd.melt(df, id_vars='SalePrice', value_vars=cat)
            g = sns.FacetGrid (p, col='variable', col_wrap=2, sharex=False, sharey=False, size=5)
            g = g.map(violinplot, 'value','SalePrice')
            g
            
            
  BAR GRAPH 
  
     df.groupby('MSZoning')['SalePrice'].agg(['mean']).plot.bar(figsize=(15,9))
     
  LOTSHAPE IS A COLUMN AND REG IS ONE OF THE CATEGORY OF COLUMN LOTSHAPE
   Reg	Regular	
   IR1	Slightly irregular
   IR2	Moderately Irregular
   IR3	Irregular
     
    df[df['LotShape']=="Reg"].SalePrice.hist(bins=10)
        
