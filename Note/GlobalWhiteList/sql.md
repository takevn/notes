

-- SELECT * FROM `reemo-173606.test.bid_20190605_uri` LIMIT 1000
--   SELECT    log.site FROM `reemo-173606.reemo_log.bid_20190606` LIMIT 3000
--     SELECT
--         COUNT(DISTINCT uids.dsp_uid) AS cnt,
--         log.rt.advertiser_id AS target_advertiser_id
--     FROM `reemo-173606.reemo_log.rt_20190505`,
--         UNNEST(log.user.uids) AS uids
--         GROUP BY log.rt.advertiser_id
--  SELECT * FROM `reemo-173606.test.bid_20190607` LIMIT 1000
SELECT
--   DISTINCT site.fqdn,
--   DOMAIN(site.url) AS user_domain,
FORMAT("%T", NET.REG_DOMAIN(site.url)) AS domain1,
NET.REG_DOMAIN(site.url) AS domain,
site.ssp_id,
site.url
FROM
`reemo-173606.test.bid_20190607`
WHERE
site.ssp_id IN (
SELECT
  MAX( site.ssp_id)
FROM
  `reemo-173606.test.bid_20190607`
GROUP BY
  site.fqdn
  )
  AND site.url IS NOT NULL
-- GROUP BY
--   domain
-- HAVING
--   domain IS NOT NULL
--   AND domain != ''


--     HOST(REPLACE(CASE WHEN url CONTAINS '//' THEN url ELSE 'http://' + url END, '&', '?')) AS output

# for test(development)
SELECT
  NET.REG_DOMAIN( site.fqdn ) AS domain,
  site.ssp_id,
  ANY_VALUE(site.url) AS url
FROM
  `reemo-173606.${REEMO_DATASET}.bid_${TARGET_DATE}`
WHERE
  site.fqdn IS NOT NULL
  AND site.fqdn != ''
GROUP BY
  domain,
  ssp_id
ORDER BY
  domain,
  ssp_id

# insert into table common_white_domain_reviews
  INSERT INTO
  common_white_domain_reviews
    (ssps_id, common_white_domains_id, review, created_at, updated_at)
VALUES
  ("${SSP_ID}", "${COMMON_WHITE_DOMAIN_ID}", 0, NOW(), NOW());

# insert into table common_white_domains
  INSERT INTO
  common_white_domains (domain, url, created_at, updated_at)
VALUES
  ("${DOMAIN}", "${URL}", NOW(), NOW())
ON
  DUPLICATE KEY
UPDATE
  id=LAST_INSERT_ID(id),
  domain=VALUES(domain),
  url=VALUES(url),
  created_at=NOW(),
  updated_at=NOW();
