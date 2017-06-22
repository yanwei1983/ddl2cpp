# ddl2cpp
convert ddl to cppstruct, need use gcc4.9+


ddl export from mysql:
```
CREATE TABLE `tbld_player` (
  `id` bigint(11) unsigned NOT NULL AUTO_INCREMENT,
  `name` varchar(32) NOT NULL DEFAULT '',
  `job` tinyint(4) NOT NULL DEFAULT '0',
  `lev` smallint(6) NOT NULL DEFAULT '0',
  `exp` int(10) unsigned NOT NULL DEFAULT '0',
  PRIMARY KEY (`id`),
  UNIQUE KEY `idx_name` (`name`),
  KEY `idx_lev` (`lev`),
  KEY `idx_job` (`job`)
) ENGINE=MyISAM DEFAULT CHARSET=latin1;

CREATE TABLE `tbld_item` (
  `id` bigint(11) unsigned NOT NULL AUTO_INCREMENT,
  `owner_id` int(10) unsigned NOT NULL DEFAULT '0',
  `itemtype` int(10) unsigned NOT NULL DEFAULT '0',
  `package_type` int(10) unsigned NOT NULL DEFAULT '0',
  `package_idx` int(10) unsigned NOT NULL DEFAULT '0',
  PRIMARY KEY (`id`),
  KEY `idx_itemtype` (`itemtype`),
  KEY `idx_owner_pack` (`owner_id`,`package_type`)
) ENGINE=MyISAM DEFAULT CHARSET=latin1;
```

end of process:

```

struct TBLD_PLAYER
{
	static const std::string table_name="tbld_player";
	enum
	{
		ID,NAME,JOB,LEV,EXP
	};
	static const std::string field_name[] = {"id","name","job","lev","exp"};
	uint64_t id;
	char[32]name;
	int8_t job;
	int16_t lev;
	uint32_t exp;
	
};

		
struct TBLD_ITEM
{
	static const std::string table_name="tbld_item";
	enum
	{
		ID,OWNER_ID,ITEMTYPE,PACKAGE_TYPE,PACKAGE_IDX
	};
	static const std::string field_name[] = {"id","owner_id","itemtype","package_type","package_idx"};
	uint64_t id;
	uint32_t owner_id;
	uint32_t itemtype;
	uint32_t package_type;
	uint32_t package_idx;
	
};

		
```


