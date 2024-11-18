## Para aumentar o tamanho do volume lógico /dev/mapper, siga os seguintes passos:

Verificar espaço disponível no Volume Group (VG):

**Utilize o comando** 

vgdisplay

para verificar se há espaço livre no Volume Group. Procure pela linha "Free PE / Size", que indica o espaço disponível no grupo de volumes.

**Expandir o Logical Volume (LV): Caso haja espaço disponível no VG, expanda o tamanho do LV utilizando o comando:**


lvextend -L +[tamanho] /dev/mapper/ubuntu--vg-ubuntu--lv


Substitua [tamanho] pelo valor que você deseja adicionar, como 10G para adicionar 10GB.

**Se preferir utilizar todo o espaço livre disponível, use:**

lvextend -l +100%FREE /dev/mapper/ubuntu--vg-ubuntu--lv.

Redimensionar o sistema de arquivos:

Após expandir o LV, redimensione o sistema de arquivos para utilizar o novo espaço.

**Para sistemas de arquivos do tipo ext4, use o comando:**

resize2fs /dev/mapper/ubuntu--vg-ubuntu--lv

**Para sistemas XFS (que não são compatíveis com resize2fs), utilize:**

xfs_growfs /ponto_de_montagem.

Confirmar a expansão: 

**Por fim, verifique se o sistema de arquivos foi redimensionado com sucesso utilizando o comando:**

df -h.
