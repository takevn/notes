Map<Integer, TreeSet<String>> mapData = replicatedMap.values()
//        Map<Integer, List<String>> mapData = replicatedMap.values()
               .stream()
//                .map(x -> ((DomainsSspIdsReviewModel) x).getReview())
               .filter(x -> ((DomainsSspIdsReviewModel) x).getReview() == 1)
//                .collect(Collectors.groupingBy(
//                        DomainsSspIdsReviewModel::getSspId,
//                        Collectors.mapping(DomainsSspIdsReviewModel::getRequestDomainsId, toList())))
               .collect(Collectors.groupingBy(
//                        DomainsSspIdsReviewModel::getSspId,
                       x -> ((DomainsSspIdsReviewModel) x).getSspId(),

//                        Collectors.mapping(DomainsSspIdsReviewModel::getRequestDomainsId, toSet()))
                       Collectors.mapping(x -> {
                           Long id = ((DomainsSspIdsReviewModel) x).getRequestDomainsId();
                           return RequestDomainModel.getModel(id).getDomain(); }, toCollection(TreeSet::new)))
               );



//                .map(x -> ((DomainsSspIdsReviewModel) x).getRequestDomainsId())
//                .map(x -> RequestDomainModel.getModel(x).getDomain())
//                .map(x -> new StringBuilder(x).reverse().toString())
//                .collect(Collectors.groupingBy((x) -> x.name, mapping((x) -> x.property, toSet())));
//                .collect(Collectors.toMap())
//                .collect(Collectors.toMap()
//                .collect(Collectors.toCollection(TreeSet::new));

# ifPresent
//        Optional<String> optional = Optional.ofNullable(model.getCommonWhiteDomainModel())
//                .map(CommonWhiteDomainModel::getDomain);
//        if (optional.isPresent()) {
//            String reversed = new StringBuilder(optional.get()).reverse().toString();
//            domainCacheMap.get(model.getSspId()).add(reversed);
//        }

        Optional.ofNullable(model.getCommonWhiteDomainModel())
                .map(CommonWhiteDomainModel::getDomain)
                .ifPresent(domain -> {
                    String reversed = new StringBuilder(domain).reverse().toString();
                    domainCacheMap.get(model.getSspId()).add(reversed);
                });

# Map<Object, Integer> collect
                Map<Object, Integer> collect = IntStream.range(0, 100000)
                        .mapToObj(i -> Roulette.choiceTrueOrFalse(10, 100 - 10))
                        .collect(Collectors.groupingBy(x -> x, Collectors.summingInt(x -> 1)));
