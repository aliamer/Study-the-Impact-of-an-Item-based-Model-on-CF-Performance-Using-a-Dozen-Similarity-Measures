# Study-the-Impact-of-an-Item-based-Model-on-CF-Performance-Using-a-Dozen-Similarity-Measures
This work comes to lay the groundwork for testing the impact of an item-based model on CF performance using a dozen similarity measures on the Movie-lens 100K and FilmTrust datasets. 
/**
 * SIM: MACHINE LEARNING ALGORITHMS FRAMEWORK
 * (C) Copyright by Loc Nguyen's Academic Network
 */
package net.hudup.alg.cf.nb;

import java.rmi.RemoteException;
import java.util.Set;

import net.hudup.core.alg.DuplicatableAlg;
import net.hudup.core.alg.RecommendParam;
import net.hudup.core.alg.cf.nb.NeighborCFItemBased;
import net.hudup.core.data.DataConfig;
import net.hudup.core.data.Profile;
import net.hudup.core.data.RatingVector;

/**
 * This class sets up an extended version of item-based nearest neighbors collaborative filtering (Neighbor CF) algorithm with more similarity measures.
 * 
 * @author Loc Nguyen
 * @version 1.0
 *
 */
public class NeighborCFExtItemBased extends NeighborCFExt implements DuplicatableAlg {

	
	/**
	 * Default serial version UID.
	 */
	private static final long serialVersionUID = 1L;

	
	/**
	 * Default constructor.
	 */
	public NeighborCFExtItemBased() {

	}


	@Override
	public RatingVector estimate(RecommendParam param, Set<Integer> queryIds) throws RemoteException {
		return NeighborCFItemBased.estimate(this, param, queryIds);
	}

	
	@Override
	protected double cod(
			RatingVector vRating1, RatingVector vRating2,
			Profile profile1, Profile profile2) {
		return cod(vRating1, vRating2, getUserMeans());
	}

	
	@Override
	protected double pipNormal(RatingVector vRating1, RatingVector vRating2, Profile profile1, Profile profile2) {
		return pipNormal(vRating1, vRating2, getUserMeans());
	}


	@Override
	protected double mpip(RatingVector vRating1, RatingVector vRating2, Profile profile1, Profile profile2) {
		return mpip(vRating1, vRating2, getUserMeans());
	}

	
	@Override
	protected double pssNormal(RatingVector vRating1, RatingVector vRating2,
			Profile profile1, Profile profile2) {
		return pssNormal(vRating1, vRating2, getUserMeans());
	}

	
	@Override
	protected double pc(RatingVector vRating1, RatingVector vRating2, Profile profile1,
			Profile profile2, int fixedColumnId) {
		return pc(vRating1, vRating2, fixedColumnId, getUserMeans());
	}


	@Override
	protected Set<Integer> getRowIds() {
		return getItemIds();
	}

	
	@Override
	protected RatingVector getRowRating(int rowId) {
		return dataset.getItemRating(rowId);
	}

	
	@Override
	protected double calcRowMean(RatingVector vRating) {
		return calcItemMean(vRating);
	}


	@Override
	protected Set<Integer> getColumnIds() {
		return getUserIds();
	}

	
	@Override
	protected RatingVector getColumnRating(int columnId) {
		return dataset.getUserRating(columnId);
	}


	@Override
	protected double calcColumnMean(RatingVector vRating) {
		return calcUserMean(vRating);
	}

	
	@Override
	protected double prob(int columnId) {
		return prob(columnId, true);
	}


	@Override
	public String getName() {
		String name = getConfig().getAsString(DUPLICATED_ALG_NAME_FIELD);
		if (name != null && !name.isEmpty())
			return name;
		else
			return "neighborcf_itembased_ext";
	}


	@Override
	public void setName(String name) {
		getConfig().put(DUPLICATED_ALG_NAME_FIELD, name);
	}

	
	@Override
	public String getDescription() throws RemoteException {
		return "Extended item-based nearest neighbors collaborative filtering algorithm";
	}


	@Override
	public DataConfig createDefaultConfig() {
		DataConfig config = super.createDefaultConfig();
		config.addReadOnly(DUPLICATED_ALG_NAME_FIELD);
		return config;
	}

	
}

The whole framework can be reached at:
 https://github.com/locnguyenacademic/sim/tree/master/3_implementation
